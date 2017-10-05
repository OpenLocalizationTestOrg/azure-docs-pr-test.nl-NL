---
title: 'Zelfstudie: Azure Active Directory-integratie met PolicyStat | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en PolicyStat.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: af5eb0f1-1c8e-4809-b0c4-8ccfb915ca42
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 704afd5515b02ce2a4fbf35da65fad74dc506271
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-policystat"></a><span data-ttu-id="2b8a8-103">Zelfstudie: Azure Active Directory-integratie met PolicyStat</span><span class="sxs-lookup"><span data-stu-id="2b8a8-103">Tutorial: Azure Active Directory integration with PolicyStat</span></span>

<span data-ttu-id="2b8a8-104">In deze zelfstudie leert u hoe PolicyStat integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2b8a8-104">In this tutorial, you learn how to integrate PolicyStat with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2b8a8-105">PolicyStat integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="2b8a8-105">Integrating PolicyStat with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2b8a8-106">U kunt beheren in Azure AD die toegang tot PolicyStat heeft</span><span class="sxs-lookup"><span data-stu-id="2b8a8-106">You can control in Azure AD who has access to PolicyStat</span></span>
- <span data-ttu-id="2b8a8-107">U kunt uw gebruikers automatisch ophalen aangemeld bij PolicyStat (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="2b8a8-107">You can enable your users to automatically get signed-on to PolicyStat (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2b8a8-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="2b8a8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2b8a8-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2b8a8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b8a8-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2b8a8-110">Prerequisites</span></span>

<span data-ttu-id="2b8a8-111">Voor het configureren van Azure AD-integratie met PolicyStat, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="2b8a8-111">To configure Azure AD integration with PolicyStat, you need the following items:</span></span>

- <span data-ttu-id="2b8a8-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="2b8a8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2b8a8-113">Een PolicyStat eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="2b8a8-113">A PolicyStat single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2b8a8-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2b8a8-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="2b8a8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2b8a8-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2b8a8-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2b8a8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2b8a8-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="2b8a8-118">Scenario description</span></span>
<span data-ttu-id="2b8a8-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2b8a8-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="2b8a8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2b8a8-121">PolicyStat uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="2b8a8-121">Adding PolicyStat from the gallery</span></span>
2. <span data-ttu-id="2b8a8-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2b8a8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-policystat-from-the-gallery"></a><span data-ttu-id="2b8a8-123">PolicyStat uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="2b8a8-123">Adding PolicyStat from the gallery</span></span>
<span data-ttu-id="2b8a8-124">Voor het configureren van de integratie van PolicyStat in Azure AD, moet u PolicyStat uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-124">To configure the integration of PolicyStat into Azure AD, you need to add PolicyStat from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2b8a8-125">**Als u wilt toevoegen PolicyStat uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="2b8a8-125">**To add PolicyStat from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2b8a8-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2b8a8-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2b8a8-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="2b8a8-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="2b8a8-133">Typ in het zoekvak **PolicyStat**.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-133">In the search box, type **PolicyStat**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_search.png)

5. <span data-ttu-id="2b8a8-135">Selecteer in het deelvenster resultaten **PolicyStat**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-135">In the results panel, select **PolicyStat**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2b8a8-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2b8a8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2b8a8-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met PolicyStat op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-138">In this section, you configure and test Azure AD single sign-on with PolicyStat based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2b8a8-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in PolicyStat is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PolicyStat is to a user in Azure AD.</span></span> <span data-ttu-id="2b8a8-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in PolicyStat tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-140">In other words, a link relationship between an Azure AD user and the related user in PolicyStat needs to be established.</span></span>

<span data-ttu-id="2b8a8-141">Wijs in PolicyStat, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-141">In PolicyStat, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2b8a8-142">Om te configureren en testen van Azure AD eenmalige aanmelding met PolicyStat, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="2b8a8-142">To configure and test Azure AD single sign-on with PolicyStat, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2b8a8-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2b8a8-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2b8a8-145">**[Maken van een testgebruiker PolicyStat](#creating-a-policystat-test-user)**  - PolicyStat die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-145">**[Creating a PolicyStat test user](#creating-a-policystat-test-user)** - to have a counterpart of Britta Simon in PolicyStat that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2b8a8-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2b8a8-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2b8a8-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="2b8a8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2b8a8-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing PolicyStat configureren.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PolicyStat application.</span></span>

<span data-ttu-id="2b8a8-150">**Voor het configureren van Azure AD eenmalige aanmelding met PolicyStat, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="2b8a8-150">**To configure Azure AD single sign-on with PolicyStat, perform the following steps:**</span></span>

1. <span data-ttu-id="2b8a8-151">In de Azure-portal op de **PolicyStat** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-151">In the Azure portal, on the **PolicyStat** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="2b8a8-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_samlbase.png)

3. <span data-ttu-id="2b8a8-155">Op de **PolicyStat domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="2b8a8-155">On the **PolicyStat Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_url.png)

    <span data-ttu-id="2b8a8-157">a.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-157">a.</span></span> <span data-ttu-id="2b8a8-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.policystat.com`</span><span class="sxs-lookup"><span data-stu-id="2b8a8-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.policystat.com`</span></span>

    <span data-ttu-id="2b8a8-159">b.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-159">b.</span></span> <span data-ttu-id="2b8a8-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.policystat.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="2b8a8-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.policystat.com/saml2/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2b8a8-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-161">These values are not real.</span></span> <span data-ttu-id="2b8a8-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="2b8a8-163">Neem contact op met [PolicyStat Client ondersteuningsteam](http://www.policystat.com/support/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-163">Contact [PolicyStat Client support team](http://www.policystat.com/support/) to get these values.</span></span> 
 
4. <span data-ttu-id="2b8a8-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_certificate.png) 

5. <span data-ttu-id="2b8a8-166">Het doel van deze sectie is om een overzicht van gebruikers om te verifiëren PolicyStat aan hun account in Azure AD dat gebruikmaakt van Federatie op basis van het SAML-protocol in staat te.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-166">The objective of this section is to outline how to enable users to authenticate to PolicyStat with their account in Azure AD using federation based on the SAML protocol.</span></span>

    <span data-ttu-id="2b8a8-167">De toepassing PolicyStat verwacht de SAML-asserties in een specifieke indeling waarvoor u het toevoegen van aangepast kenmerktoewijzingen aan uw **SAML-Token kenmerken** configuratie.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-167">The PolicyStat application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.</span></span>  

     <span data-ttu-id="2b8a8-168">De volgende Schermafbeelding toont een voorbeeld hiervan.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-168">The following screenshot shows an example of this.</span></span>

     <span data-ttu-id="2b8a8-169">![Kenmerken](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "kenmerken")</span><span class="sxs-lookup"><span data-stu-id="2b8a8-169">![Attributes](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "Attributes")</span></span>

6. <span data-ttu-id="2b8a8-170">Als u wilt de vereiste kenmerktoewijzingen toevoegen, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="2b8a8-170">To add the required attribute mappings, perform the following steps:</span></span>

    | <span data-ttu-id="2b8a8-171">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="2b8a8-171">Attribute Name</span></span>    |   <span data-ttu-id="2b8a8-172">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="2b8a8-172">Attribute Value</span></span> |
    |------------------- | -------------------- |
    | <span data-ttu-id="2b8a8-173">UID</span><span class="sxs-lookup"><span data-stu-id="2b8a8-173">uid</span></span> | <span data-ttu-id="2b8a8-174">ExtractMailPrefix([mail])</span><span class="sxs-lookup"><span data-stu-id="2b8a8-174">ExtractMailPrefix([mail])</span></span> |
    
    <span data-ttu-id="2b8a8-175">a.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-175">a.</span></span> <span data-ttu-id="2b8a8-176">Klik op **toevoegen kenmerk** openen de **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addatribute.png)
    
    <span data-ttu-id="2b8a8-179">b.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-179">b.</span></span> <span data-ttu-id="2b8a8-180">In de **kenmerknaam** textbox type **uid**.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-180">In the **Attribute Name** textbox, type **uid**.</span></span>

    <span data-ttu-id="2b8a8-181">c.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-181">c.</span></span> <span data-ttu-id="2b8a8-182">In de **kenmerkwaarde** textbox, selecteer **ExtractMailPrefix()**.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-182">In the **Attribute Value** textbox, select **ExtractMailPrefix()**.</span></span>    
   
    <span data-ttu-id="2b8a8-183">d.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-183">d.</span></span> <span data-ttu-id="2b8a8-184">Van de **Mail** selecteert **User.mail**.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-184">From the **Mail** list, select **User.mail**.</span></span>
    
    <span data-ttu-id="2b8a8-185">e.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-185">e.</span></span> <span data-ttu-id="2b8a8-186">Klik op **Ok**</span><span class="sxs-lookup"><span data-stu-id="2b8a8-186">Click **Ok**</span></span>

7. <span data-ttu-id="2b8a8-187">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-187">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-policystat-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="2b8a8-189">In een ander browservenster, meld u bij uw bedrijf PolicyStat site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-189">In a different web browser window, log into your PolicyStat company site as an administrator.</span></span>

9. <span data-ttu-id="2b8a8-190">Klik op de **Admin** tabblad en klik vervolgens op **configuratie voor één aanmelding** in het navigatiedeelvenster links.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-190">Click the **Admin** tab, and then click **Single Sign-On Configuration** in left navigation pane.</span></span>
   
    <span data-ttu-id="2b8a8-191">![Menu beheerder](./media/active-directory-saas-policystat-tutorial/ic808633.png "Menu beheerder")</span><span class="sxs-lookup"><span data-stu-id="2b8a8-191">![Administrator Menu](./media/active-directory-saas-policystat-tutorial/ic808633.png "Administrator Menu")</span></span>

10. <span data-ttu-id="2b8a8-192">In de **Setup** sectie **inschakelen eenmalige aanmelding integratie**.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-192">In the **Setup** section, select **Enable Single Sign-on Integration**.</span></span>
   
    <span data-ttu-id="2b8a8-193">![Eenmalige aanmelding configuratie](./media/active-directory-saas-policystat-tutorial/ic808634.png "Single Sign-On-configuratie")</span><span class="sxs-lookup"><span data-stu-id="2b8a8-193">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808634.png "Single Sign-On Configuration")</span></span>

11. <span data-ttu-id="2b8a8-194">Klik op **kenmerken configureren**, en klikt u op de **kenmerken configureren** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="2b8a8-194">Click **Configure Attributes**, and then, in the **Configure Attributes** section, perform the following steps:</span></span>
   
    <span data-ttu-id="2b8a8-195">![Eenmalige aanmelding configuratie](./media/active-directory-saas-policystat-tutorial/ic808635.png "Single Sign-On-configuratie")</span><span class="sxs-lookup"><span data-stu-id="2b8a8-195">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808635.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="2b8a8-196">a.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-196">a.</span></span> <span data-ttu-id="2b8a8-197">In de **kenmerk Username** textbox type **uid**.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-197">In the **Username Attribute** textbox, type **uid**.</span></span>

    <span data-ttu-id="2b8a8-198">b.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-198">b.</span></span> <span data-ttu-id="2b8a8-199">In de **voornaam kenmerk** textbox type **firstname** van gebruiker **Britta**.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-199">In the **First Name Attribute** textbox, type **firstname** of user **Britta**.</span></span>

    <span data-ttu-id="2b8a8-200">c.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-200">c.</span></span> <span data-ttu-id="2b8a8-201">In de **laatste naamkenmerk** textbox type **lastname** van gebruiker **Simon**.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-201">In the **Last Name Attribute** textbox, type **lastname** of user **Simon**.</span></span>

    <span data-ttu-id="2b8a8-202">d.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-202">d.</span></span> <span data-ttu-id="2b8a8-203">In de **e kenmerk** textbox type **emailaddress** van gebruiker  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="2b8a8-203">In the **Email Attribute** textbox, type **emailaddress** of user **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="2b8a8-204">e.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-204">e.</span></span> <span data-ttu-id="2b8a8-205">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-205">Click **Save Changes**.</span></span>

12. <span data-ttu-id="2b8a8-206">Klik op **uw IDP metagegevens**, en klikt u op de **uw IDP metagegevens** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="2b8a8-206">Click **Your IDP Metadata**, and then, in the **Your IDP Metadata** section, perform the following steps:</span></span>
   
    <span data-ttu-id="2b8a8-207">![Eenmalige aanmelding configuratie](./media/active-directory-saas-policystat-tutorial/ic808636.png "Single Sign-On-configuratie")</span><span class="sxs-lookup"><span data-stu-id="2b8a8-207">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808636.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="2b8a8-208">a.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-208">a.</span></span> <span data-ttu-id="2b8a8-209">Uw gedownloade metagegevensbestand openen, de inhoud kopieert en plakt u deze in de **uw identiteit Provider metagegevens** textbox.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-209">Open your downloaded metadata file, copy the content, and  then paste it into the **Your Identity Provider Metadata** textbox.</span></span>

    <span data-ttu-id="2b8a8-210">b.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-210">b.</span></span> <span data-ttu-id="2b8a8-211">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-211">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="2b8a8-212">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="2b8a8-212">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2b8a8-213">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-213">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2b8a8-214">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2b8a8-214">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2b8a8-215">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="2b8a8-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="2b8a8-216">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-216">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="2b8a8-218">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="2b8a8-218">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2b8a8-219">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-219">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-policystat-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2b8a8-221">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-221">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-policystat-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2b8a8-223">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-223">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-policystat-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2b8a8-225">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="2b8a8-225">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-policystat-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2b8a8-227">a.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-227">a.</span></span> <span data-ttu-id="2b8a8-228">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-228">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2b8a8-229">b.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-229">b.</span></span> <span data-ttu-id="2b8a8-230">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-230">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2b8a8-231">c.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-231">c.</span></span> <span data-ttu-id="2b8a8-232">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-232">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2b8a8-233">d.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-233">d.</span></span> <span data-ttu-id="2b8a8-234">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-234">Click **Create**.</span></span>
 
### <a name="creating-a-policystat-test-user"></a><span data-ttu-id="2b8a8-235">Een testgebruiker PolicyStat maken</span><span class="sxs-lookup"><span data-stu-id="2b8a8-235">Creating a PolicyStat test user</span></span>

<span data-ttu-id="2b8a8-236">Om in te schakelen gebruikers van Azure AD aan te melden bij PolicyStat, moeten ze worden ingericht in PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-236">In order to enable Azure AD users to log into PolicyStat, they must be provisioned into PolicyStat.</span></span>  

<span data-ttu-id="2b8a8-237">PolicyStat ondersteunt alleen in de tijd van gebruikersinrichting.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-237">PolicyStat supports just in time user provisioning.</span></span> <span data-ttu-id="2b8a8-238">Dit houdt in dat u niet hoeft de gebruikers handmatig toevoegen aan PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-238">This means, you do not need to add the users manually to PolicyStat.</span></span> <span data-ttu-id="2b8a8-239">De gebruikers wordt automatisch ophalen toegevoegd aan de eerste aanmelding via eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-239">The users will get added automatically on their first login through SSO.</span></span>

>[!NOTE]
><span data-ttu-id="2b8a8-240">U kunt andere PolicyStat gebruiker account hulpmiddelen voor het maken of API's die is geleverd door PolicyStat voor het inrichten van Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-240">You can use any other PolicyStat user account creation tools or APIs provided by PolicyStat to provision Azure AD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2b8a8-241">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b8a8-241">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2b8a8-242">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PolicyStat.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="2b8a8-244">**Britta Simon om aan te wijzen PolicyStat, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="2b8a8-244">**To assign Britta Simon to PolicyStat, perform the following steps:**</span></span>

1. <span data-ttu-id="2b8a8-245">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="2b8a8-247">Selecteer in de lijst met toepassingen **PolicyStat**.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-247">In the applications list, select **PolicyStat**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_app.png) 

3. <span data-ttu-id="2b8a8-249">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-249">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="2b8a8-251">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-251">Click **Add** button.</span></span> <span data-ttu-id="2b8a8-252">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="2b8a8-254">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2b8a8-255">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2b8a8-256">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2b8a8-257">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="2b8a8-257">Testing single sign-on</span></span>

<span data-ttu-id="2b8a8-258">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2b8a8-259">Als u op de tegel PolicyStat in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="2b8a8-259">When you click the PolicyStat tile in the Access Panel, you should get automatically signed-on to your PolicyStat application.</span></span>
<span data-ttu-id="2b8a8-260">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2b8a8-260">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2b8a8-261">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="2b8a8-261">Additional resources</span></span>

* [<span data-ttu-id="2b8a8-262">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2b8a8-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2b8a8-263">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2b8a8-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_203.png

