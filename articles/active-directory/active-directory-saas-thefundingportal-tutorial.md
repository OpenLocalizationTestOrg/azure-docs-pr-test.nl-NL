---
title: 'Zelfstudie: Azure Active Directory-integratie met de Portal middelen | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en de middelen Portal.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4663cc8a-976a-4c6c-b3b4-1e5df9b66744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: d0bfc793bb26c551f85706eaec857962a3415e1f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-the-funding-portal"></a><span data-ttu-id="09448-103">Zelfstudie: Azure Active Directory-integratie met de middelen Portal</span><span class="sxs-lookup"><span data-stu-id="09448-103">Tutorial: Azure Active Directory integration with The Funding Portal</span></span>

<span data-ttu-id="09448-104">In deze zelfstudie leert u hoe de middelen Portal integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="09448-104">In this tutorial, you learn how to integrate The Funding Portal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="09448-105">De middelen Portal integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="09448-105">Integrating The Funding Portal with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="09448-106">U kunt beheren in Azure AD die toegang tot de middelen Portal heeft</span><span class="sxs-lookup"><span data-stu-id="09448-106">You can control in Azure AD who has access to The Funding Portal</span></span>
- <span data-ttu-id="09448-107">U kunt uw gebruikers automatisch ophalen aangemeld bij de middelen Portal (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="09448-107">You can enable your users to automatically get signed-on to The Funding Portal (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="09448-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="09448-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="09448-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="09448-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09448-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="09448-110">Prerequisites</span></span>

<span data-ttu-id="09448-111">Voor het configureren van Azure AD-integratie met de middelen Portal, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="09448-111">To configure Azure AD integration with The Funding Portal, you need the following items:</span></span>

- <span data-ttu-id="09448-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="09448-112">An Azure AD subscription</span></span>
- <span data-ttu-id="09448-113">Een Portal van de middelen eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="09448-113">A The Funding Portal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="09448-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="09448-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="09448-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="09448-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="09448-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="09448-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="09448-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="09448-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="09448-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="09448-118">Scenario description</span></span>
<span data-ttu-id="09448-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="09448-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="09448-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="09448-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="09448-121">Toevoegen van de Portal van de middelen uit de galerie</span><span class="sxs-lookup"><span data-stu-id="09448-121">Adding The Funding Portal from the gallery</span></span>
2. <span data-ttu-id="09448-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="09448-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-the-funding-portal-from-the-gallery"></a><span data-ttu-id="09448-123">Toevoegen van de Portal van de middelen uit de galerie</span><span class="sxs-lookup"><span data-stu-id="09448-123">Adding The Funding Portal from the gallery</span></span>
<span data-ttu-id="09448-124">Voor het configureren van de integratie van de Portal die middelen in Azure AD, moet u de middelen Portal uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="09448-124">To configure the integration of The Funding Portal into Azure AD, you need to add The Funding Portal from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="09448-125">**Als u wilt de middelen Portal uit de galerie toevoegen, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="09448-125">**To add The Funding Portal from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="09448-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="09448-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="09448-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="09448-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="09448-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="09448-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="09448-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="09448-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="09448-133">Typ in het zoekvak **de middelen Portal**.</span><span class="sxs-lookup"><span data-stu-id="09448-133">In the search box, type **The Funding Portal**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_search.png)

5. <span data-ttu-id="09448-135">Selecteer in het deelvenster resultaten **de middelen Portal**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="09448-135">In the results panel, select **The Funding Portal**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="09448-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="09448-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="09448-138">In deze sectie die u kunt configureren en testen Azure AD eenmalige aanmelding met de middelen-Portal op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="09448-138">In this section, you configure and test Azure AD single sign-on with The Funding Portal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="09448-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in de Portal die middelen in Azure AD voor een gebruiker is.</span><span class="sxs-lookup"><span data-stu-id="09448-139">For single sign-on to work, Azure AD needs to know what the counterpart user in The Funding Portal is to a user in Azure AD.</span></span> <span data-ttu-id="09448-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in de Portal middelen tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="09448-140">In other words, a link relationship between an Azure AD user and the related user in The Funding Portal needs to be established.</span></span>

<span data-ttu-id="09448-141">In de Portal die middelen, wijs de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="09448-141">In The Funding Portal, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="09448-142">Om te configureren en testen van Azure AD eenmalige aanmelding met de middelen Portal, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="09448-142">To configure and test Azure AD single sign-on with The Funding Portal, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="09448-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="09448-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="09448-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="09448-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="09448-145">**[Maken van de Portal middelen testgebruiker](#creating-the-funding-portal-test-user)**  : een equivalent van Britta Simon hebben in de Portal middelen die is gekoppeld aan de Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="09448-145">**[Creating The Funding Portal test user](#creating-the-funding-portal-test-user)** - to have a counterpart of Britta Simon in The Funding Portal that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="09448-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="09448-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="09448-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="09448-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="09448-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="09448-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="09448-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing de middelen Portal configureren.</span><span class="sxs-lookup"><span data-stu-id="09448-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your The Funding Portal application.</span></span>

<span data-ttu-id="09448-150">**Voor het configureren van Azure AD eenmalige aanmelding met de middelen Portal, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="09448-150">**To configure Azure AD single sign-on with The Funding Portal, perform the following steps:**</span></span>

1. <span data-ttu-id="09448-151">In de Azure-portal op de **de middelen Portal** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="09448-151">In the Azure portal, on the **The Funding Portal** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="09448-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="09448-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_samlbase.png)

3. <span data-ttu-id="09448-155">Op de **URL's en -Portal van de middelen domein** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="09448-155">On the **The Funding Portal Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_url.png)

    <span data-ttu-id="09448-157">a.</span><span class="sxs-lookup"><span data-stu-id="09448-157">a.</span></span> <span data-ttu-id="09448-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.regenteducation.net/`</span><span class="sxs-lookup"><span data-stu-id="09448-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.regenteducation.net/`</span></span>

    <span data-ttu-id="09448-159">b.</span><span class="sxs-lookup"><span data-stu-id="09448-159">b.</span></span> <span data-ttu-id="09448-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.regenteducation.net`</span><span class="sxs-lookup"><span data-stu-id="09448-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.regenteducation.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="09448-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="09448-161">These values are not real.</span></span> <span data-ttu-id="09448-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="09448-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="09448-163">Neem contact op met [de middelen Portal Client ondersteuningsteam](mailto:info@regenteducation.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="09448-163">Contact [The Funding Portal Client support team](mailto:info@regenteducation.com) to get these values.</span></span> 

4. <span data-ttu-id="09448-164">De toepassing middelen Portal verwacht de SAML-asserties bevat een kenmerk genaamd 'externalId1'.</span><span class="sxs-lookup"><span data-stu-id="09448-164">The Funding Portal application expects the SAML assertions to contain an attribute named "externalId1".</span></span> <span data-ttu-id="09448-165">De waarde van 'externalId1' moet een erkende studentID.</span><span class="sxs-lookup"><span data-stu-id="09448-165">The value of "externalId1" should be a recognized studentID.</span></span> <span data-ttu-id="09448-166">Configureer de claim 'externalId1' voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="09448-166">Configure the "externalId1" claim for this application.</span></span> <span data-ttu-id="09448-167">U kunt de waarden van deze kenmerken van beheren de **gebruikerskenmerken** van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="09448-167">You can manage the values of these attributes from the **User Attributes** of the application.</span></span> <span data-ttu-id="09448-168">De volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="09448-168">The following screenshot shows an example for this.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_attribute.png)

5. <span data-ttu-id="09448-170">In de **gebruikerskenmerken** sectie op de **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in de afbeelding en de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="09448-170">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>

    | <span data-ttu-id="09448-171">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="09448-171">Attribute Name</span></span> | <span data-ttu-id="09448-172">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="09448-172">Attribute Value</span></span> |
    | ------------------- | ---------------- |
    | <span data-ttu-id="09448-173">externalId1</span><span class="sxs-lookup"><span data-stu-id="09448-173">externalId1</span></span> | <span data-ttu-id="09448-174">User.extensionattribute1</span><span class="sxs-lookup"><span data-stu-id="09448-174">user.extensionattribute1</span></span> |

    <span data-ttu-id="09448-175">a.</span><span class="sxs-lookup"><span data-stu-id="09448-175">a.</span></span> <span data-ttu-id="09448-176">Klik op **toevoegen kenmerk** openen de **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="09448-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thefundingportal-tutorial/tutorial_attribute_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thefundingportal-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="09448-179">b.</span><span class="sxs-lookup"><span data-stu-id="09448-179">b.</span></span> <span data-ttu-id="09448-180">In de **naam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="09448-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="09448-181">c.</span><span class="sxs-lookup"><span data-stu-id="09448-181">c.</span></span> <span data-ttu-id="09448-182">Van de **kenmerkwaarde** , selecteert u het kenmerk dat u wilt gebruiken voor uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="09448-182">From the **Attribute Value** list, select the attribute you want to use for your implementation.</span></span> <span data-ttu-id="09448-183">Bijvoorbeeld, als u de waarde StudentID in de ExtensionAttribute1 hebt opgeslagen, selecteert u user.extensionattribute1.</span><span class="sxs-lookup"><span data-stu-id="09448-183">For example, if you have stored the StudentID value in the ExtensionAttribute1, then select user.extensionattribute1.</span></span>
    
    <span data-ttu-id="09448-184">d.</span><span class="sxs-lookup"><span data-stu-id="09448-184">d.</span></span> <span data-ttu-id="09448-185">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="09448-185">Click **Ok**.</span></span>
 
6. <span data-ttu-id="09448-186">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="09448-186">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_certificate.png) 

7. <span data-ttu-id="09448-188">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="09448-188">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="09448-190">Eenmalige aanmelding configureren op **de middelen Portal** zijde, moet u de gedownloade verzenden **Metadata XML** naar [de middelen Portal ondersteuningsteam](mailto:info@regenteducation.com).</span><span class="sxs-lookup"><span data-stu-id="09448-190">To configure single sign-on on **The Funding Portal** side, you need to send the downloaded **Metadata XML** to [The Funding Portal support team](mailto:info@regenteducation.com).</span></span> <span data-ttu-id="09448-191">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="09448-191">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="09448-192">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="09448-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="09448-193">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="09448-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="09448-194">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="09448-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="09448-195">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="09448-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="09448-196">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="09448-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="09448-198">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="09448-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="09448-199">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="09448-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="09448-201">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="09448-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="09448-203">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="09448-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="09448-205">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="09448-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="09448-207">a.</span><span class="sxs-lookup"><span data-stu-id="09448-207">a.</span></span> <span data-ttu-id="09448-208">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="09448-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="09448-209">b.</span><span class="sxs-lookup"><span data-stu-id="09448-209">b.</span></span> <span data-ttu-id="09448-210">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="09448-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="09448-211">c.</span><span class="sxs-lookup"><span data-stu-id="09448-211">c.</span></span> <span data-ttu-id="09448-212">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="09448-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="09448-213">d.</span><span class="sxs-lookup"><span data-stu-id="09448-213">d.</span></span> <span data-ttu-id="09448-214">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="09448-214">Click **Create**.</span></span>
 
### <a name="creating-the-funding-portal-test-user"></a><span data-ttu-id="09448-215">De middelen Portal testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="09448-215">Creating The Funding Portal test user</span></span>

<span data-ttu-id="09448-216">In deze sectie maakt u Britta Simon aangeroepen in de Portal middelen van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="09448-216">In this section, you create a user called Britta Simon in The Funding Portal.</span></span> <span data-ttu-id="09448-217">Werken met [de middelen Portal ondersteuningsteam](mailto:info@regenteducation.com) toe te voegen van de testgebruiker en eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="09448-217">Work with [The Funding Portal support team](mailto:info@regenteducation.com) to add the test user and enable SSO.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="09448-218">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="09448-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="09448-219">In deze sectie maakt inschakelen u Britta Simon Azure eenmalige aanmelding gebruiken door het verlenen van toegang tot de Portal middelen.</span><span class="sxs-lookup"><span data-stu-id="09448-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to The Funding Portal.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="09448-221">**Britta Simon om aan te wijzen de middelen Portal, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="09448-221">**To assign Britta Simon to The Funding Portal, perform the following steps:**</span></span>

1. <span data-ttu-id="09448-222">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="09448-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="09448-224">Selecteer in de lijst met toepassingen **de middelen Portal**.</span><span class="sxs-lookup"><span data-stu-id="09448-224">In the applications list, select **The Funding Portal**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_app.png) 

3. <span data-ttu-id="09448-226">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="09448-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="09448-228">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="09448-228">Click **Add** button.</span></span> <span data-ttu-id="09448-229">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="09448-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="09448-231">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="09448-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="09448-232">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="09448-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="09448-233">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="09448-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="09448-234">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="09448-234">Testing single sign-on</span></span>

<span data-ttu-id="09448-235">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="09448-235">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="09448-236">Als u op de tegel Portal van de middelen in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing de middelen Portal.</span><span class="sxs-lookup"><span data-stu-id="09448-236">When you click the The Funding Portal tile in the Access Panel, you should get automatically signed-on to your The Funding Portal application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="09448-237">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="09448-237">Additional resources</span></span>

* [<span data-ttu-id="09448-238">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="09448-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="09448-239">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="09448-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_203.png

