---
title: 'Zelfstudie: Azure Active Directory-integratie met Work.com | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Work.com.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 98e6739e-eb24-46bd-9dd3-20b489839076
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 7cfec8e9ac12d43095483696a15c0580776d3114
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workcom"></a><span data-ttu-id="37533-103">Zelfstudie: Azure Active Directory-integratie met Work.com</span><span class="sxs-lookup"><span data-stu-id="37533-103">Tutorial: Azure Active Directory integration with Work.com</span></span>

<span data-ttu-id="37533-104">In deze zelfstudie leert u hoe Work.com integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="37533-104">In this tutorial, you learn how to integrate Work.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="37533-105">Work.com integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="37533-105">Integrating Work.com with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="37533-106">U kunt beheren in Azure AD die toegang tot Work.com heeft</span><span class="sxs-lookup"><span data-stu-id="37533-106">You can control in Azure AD who has access to Work.com</span></span>
- <span data-ttu-id="37533-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Work.com (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="37533-107">You can enable your users to automatically get signed-on to Work.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="37533-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="37533-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="37533-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="37533-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37533-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="37533-110">Prerequisites</span></span>

<span data-ttu-id="37533-111">Voor het configureren van Azure AD-integratie met Work.com, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="37533-111">To configure Azure AD integration with Work.com, you need the following items:</span></span>

- <span data-ttu-id="37533-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="37533-112">An Azure AD subscription</span></span>
- <span data-ttu-id="37533-113">Een Work.com eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="37533-113">A Work.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="37533-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="37533-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="37533-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="37533-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="37533-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="37533-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="37533-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="37533-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="37533-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="37533-118">Scenario description</span></span>
<span data-ttu-id="37533-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="37533-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="37533-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="37533-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="37533-121">Work.com uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="37533-121">Add Work.com from the gallery</span></span>
2. <span data-ttu-id="37533-122">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="37533-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-workcom-from-the-gallery"></a><span data-ttu-id="37533-123">Work.com uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="37533-123">Add Work.com from the gallery</span></span>
<span data-ttu-id="37533-124">Voor het configureren van de integratie van Work.com in Azure AD, moet u Work.com uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="37533-124">To configure the integration of Work.com into Azure AD, you need to add Work.com from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="37533-125">**Als u wilt toevoegen Work.com uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="37533-125">**To add Work.com from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="37533-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="37533-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="37533-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="37533-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="37533-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="37533-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="37533-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="37533-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="37533-133">Typ in het zoekvak **Work.com**, selecteer **Work.com** Klik vanuit het deelvenster resultaten **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="37533-133">In the search box, type **Work.com**, select **Work.com** from results panel then click **Add** button to add the application.</span></span>

    ![Uit de galerie toevoegen](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="37533-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="37533-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="37533-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met Work.com op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="37533-136">In this section, you configure and test Azure AD single sign-on with Work.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="37533-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Work.com is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="37533-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Work.com is to a user in Azure AD.</span></span> <span data-ttu-id="37533-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Work.com tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="37533-138">In other words, a link relationship between an Azure AD user and the related user in Work.com needs to be established.</span></span>

<span data-ttu-id="37533-139">Wijs in Work.com, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="37533-139">In Work.com, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="37533-140">Om te configureren en testen van Azure AD eenmalige aanmelding met Work.com, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="37533-140">To configure and test Azure AD single sign-on with Work.com, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="37533-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="37533-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="37533-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="37533-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="37533-143">**[Maak een testgebruiker Work.com](#create-a-workcom-test-user)**  - Work.com die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="37533-143">**[Create a Work.com test user](#create-a-workcom-test-user)** - to have a counterpart of Britta Simon in Work.com that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="37533-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="37533-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="37533-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="37533-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="37533-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="37533-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="37533-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Work.com configureren.</span><span class="sxs-lookup"><span data-stu-id="37533-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Work.com application.</span></span>

>[!NOTE]
><span data-ttu-id="37533-148">Voor het configureren van eenmalige aanmelding, moet u een aangepaste domeinnaam van Work.com nog instellen.</span><span class="sxs-lookup"><span data-stu-id="37533-148">To configure single sign-on, you need to setup a custom Work.com domain name yet.</span></span> <span data-ttu-id="37533-149">U moet ten minste een domeinnaam definiëren, testen van uw domeinnaam en deze implementeren voor uw hele organisatie.</span><span class="sxs-lookup"><span data-stu-id="37533-149">You need to define at least a domain name, test your domain name, and deploy it to your entire organization.</span></span>

<span data-ttu-id="37533-150">**Voor het configureren van Azure AD eenmalige aanmelding met Work.com, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="37533-150">**To configure Azure AD single sign-on with Work.com, perform the following steps:**</span></span>

1. <span data-ttu-id="37533-151">In de Azure-portal op de **Work.com** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="37533-151">In the Azure portal, on the **Work.com** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="37533-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="37533-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Op basis van SAML eenmalige aanmelding](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_samlbase.png)

3. <span data-ttu-id="37533-155">Op de **Work.com domein en de URL's** sectie, voert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="37533-155">On the **Work.com Domain and URLs** section, perform the following:</span></span>

    ![Sectie Work.com domein en URL 's](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_url.png)

    <span data-ttu-id="37533-157">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`http://<companyname>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="37533-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<companyname>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="37533-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="37533-158">This value is not real.</span></span> <span data-ttu-id="37533-159">Deze waarde bijwerken met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="37533-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="37533-160">Neem contact op met [Work.com Client ondersteuningsteam](https://help.salesforce.com/articleView?id=000159855&type=3) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="37533-160">Contact [Work.com Client support team](https://help.salesforce.com/articleView?id=000159855&type=3) to get this value.</span></span> 

4. <span data-ttu-id="37533-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="37533-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Certificaat voor ondertekening van SAML-sectie](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_certificate.png) 

5. <span data-ttu-id="37533-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="37533-163">Click **Save** button.</span></span>

    ![De knop Opslaan](./media/active-directory-saas-work-com-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="37533-165">Op de **Work.com configuratie** sectie, klikt u op **configureren Work.com** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="37533-165">On the **Work.com Configuration** section, click **Configure Work.com** to open **Configure sign-on** window.</span></span> <span data-ttu-id="37533-166">Kopieer de **Sign-Out-URL, SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="37533-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![De configuratiesectie Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_configure.png) 
7. <span data-ttu-id="37533-168">Aanmelden bij uw tenant Work.com als administrator.</span><span class="sxs-lookup"><span data-stu-id="37533-168">Log in to your Work.com tenant as administrator.</span></span>

8. <span data-ttu-id="37533-169">Ga naar **Setup**.</span><span class="sxs-lookup"><span data-stu-id="37533-169">Go to **Setup**.</span></span>
   
    <span data-ttu-id="37533-170">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span><span class="sxs-lookup"><span data-stu-id="37533-170">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

9. <span data-ttu-id="37533-171">In het navigatiedeelvenster links in de **beheren** sectie, klikt u op **domeinbeheer** Vouw de bijbehorende sectie en klik vervolgens op **mijn domein** openen van de **Mijn domein** pagina.</span><span class="sxs-lookup"><span data-stu-id="37533-171">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
   
    <span data-ttu-id="37533-172">![Mijn domein](./media/active-directory-saas-work-com-tutorial/ic767825.png "mijn domein")</span><span class="sxs-lookup"><span data-stu-id="37533-172">![My Domain](./media/active-directory-saas-work-com-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="37533-173">Om te controleren of uw domein correct is ingesteld, zorg ervoor dat deze wordt '**stap 4 geïmplementeerd naar gebruikers**' en bekijk uw '**mijn domeininstellingen**'.</span><span class="sxs-lookup"><span data-stu-id="37533-173">To verify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed to Users**” and review your “**My Domain Settings**”.</span></span>
   
    <span data-ttu-id="37533-174">![Domein geïmplementeerd voor gebruiker](./media/active-directory-saas-work-com-tutorial/ic784377.png "domein geïmplementeerd voor gebruiker")</span><span class="sxs-lookup"><span data-stu-id="37533-174">![Domain Deployed to User](./media/active-directory-saas-work-com-tutorial/ic784377.png "Domain Deployed to User")</span></span>

11. <span data-ttu-id="37533-175">Aanmelden bij uw tenant Work.com.</span><span class="sxs-lookup"><span data-stu-id="37533-175">Log in to your Work.com tenant.</span></span>

12. <span data-ttu-id="37533-176">Ga naar **Setup**.</span><span class="sxs-lookup"><span data-stu-id="37533-176">Go to **Setup**.</span></span>
    
    <span data-ttu-id="37533-177">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span><span class="sxs-lookup"><span data-stu-id="37533-177">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

13. <span data-ttu-id="37533-178">Vouw de **beveiligingsmechanismen** menu en klik vervolgens op **instellingen voor eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="37533-178">Expand the **Security Controls** menu, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="37533-179">![Eenmalige aanmelding instellingen](./media/active-directory-saas-work-com-tutorial/ic794113.png "eenmalige aanmelding-instellingen")</span><span class="sxs-lookup"><span data-stu-id="37533-179">![Single Sign-On Settings](./media/active-directory-saas-work-com-tutorial/ic794113.png "Single Sign-On Settings")</span></span>

14. <span data-ttu-id="37533-180">Op de **instellingen voor eenmalige aanmelding** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="37533-180">On the **Single Sign-On Settings** dialog page, perform the following steps:</span></span>
    
    <span data-ttu-id="37533-181">![SAML ingeschakeld](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML ingeschakeld")</span><span class="sxs-lookup"><span data-stu-id="37533-181">![SAML Enabled](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML Enabled")</span></span>
    
    <span data-ttu-id="37533-182">a.</span><span class="sxs-lookup"><span data-stu-id="37533-182">a.</span></span> <span data-ttu-id="37533-183">Selecteer **SAML ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="37533-183">Select **SAML Enabled**.</span></span>
    
    <span data-ttu-id="37533-184">b.</span><span class="sxs-lookup"><span data-stu-id="37533-184">b.</span></span> <span data-ttu-id="37533-185">Klik op **Nieuw**.</span><span class="sxs-lookup"><span data-stu-id="37533-185">Click **New**.</span></span>

15. <span data-ttu-id="37533-186">In de **SAML Single Sign-On-instellingen** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="37533-186">In the **SAML Single Sign-On Settings** section, perform the following steps:</span></span>
    
    <span data-ttu-id="37533-187">![Afzonderlijke SAML aanmelding instelling](./media/active-directory-saas-work-com-tutorial/ic794114.png "SAML Single Sign-On-instelling")</span><span class="sxs-lookup"><span data-stu-id="37533-187">![SAML Single Sign-On Setting](./media/active-directory-saas-work-com-tutorial/ic794114.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="37533-188">a.</span><span class="sxs-lookup"><span data-stu-id="37533-188">a.</span></span> <span data-ttu-id="37533-189">In de **naam** textbox, typ een naam voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="37533-189">In the **Name** textbox, type a name for your configuration.</span></span>  
       
    > [!NOTE]
    > <span data-ttu-id="37533-190">Om een waarde voor **naam** automatisch invullen de **API-naam** textbox.</span><span class="sxs-lookup"><span data-stu-id="37533-190">Providing a value for **Name** does automatically populate the **API Name** textbox.</span></span>
    
    <span data-ttu-id="37533-191">b.</span><span class="sxs-lookup"><span data-stu-id="37533-191">b.</span></span> <span data-ttu-id="37533-192">In **verlener** textbox, plak de waarde van **SAML entiteit-ID** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="37533-192">In **Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="37533-193">c.</span><span class="sxs-lookup"><span data-stu-id="37533-193">c.</span></span> <span data-ttu-id="37533-194">Als u wilt uploaden het gedownloade certificaat vanuit Azure-portal, klikt u op **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="37533-194">To upload the downloaded certificate from Azure portal, click **Browse**.</span></span>
    
    <span data-ttu-id="37533-195">d.</span><span class="sxs-lookup"><span data-stu-id="37533-195">d.</span></span> <span data-ttu-id="37533-196">In de **entiteit-Id** textbox type `https://salesforce-work.com`.</span><span class="sxs-lookup"><span data-stu-id="37533-196">In the **Entity Id** textbox, type `https://salesforce-work.com`.</span></span>
    
    <span data-ttu-id="37533-197">e.</span><span class="sxs-lookup"><span data-stu-id="37533-197">e.</span></span> <span data-ttu-id="37533-198">Als **SAML identiteitstype**, selecteer **Assertion bevat de Federation-ID van het gebruikersobject**.</span><span class="sxs-lookup"><span data-stu-id="37533-198">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span>
    
    <span data-ttu-id="37533-199">f.</span><span class="sxs-lookup"><span data-stu-id="37533-199">f.</span></span> <span data-ttu-id="37533-200">Als **SAML identiteit locatie**, selecteer **identiteit is in het element NameIdentfier van het onderwerp overzicht**.</span><span class="sxs-lookup"><span data-stu-id="37533-200">As **SAML Identity Location**, select **Identity is in the NameIdentfier element of the Subject statement**.</span></span>
    
    <span data-ttu-id="37533-201">g.</span><span class="sxs-lookup"><span data-stu-id="37533-201">g.</span></span> <span data-ttu-id="37533-202">In **identiteit Provider aanmeldings-URL** textbox, plak de waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="37533-202">In **Identity Provider Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="37533-203">h.</span><span class="sxs-lookup"><span data-stu-id="37533-203">h.</span></span> <span data-ttu-id="37533-204">In **identiteit Provider afmelding URL** textbox, plak de waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="37533-204">In **Identity Provider Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="37533-205">ik.</span><span class="sxs-lookup"><span data-stu-id="37533-205">i.</span></span> <span data-ttu-id="37533-206">Als **Provider geïnitieerd aanvragen servicebinding**, selecteer **HTTP Post**.</span><span class="sxs-lookup"><span data-stu-id="37533-206">As **Service Provider Initiated Request Binding**, select **HTTP Post**.</span></span>
    
    <span data-ttu-id="37533-207">j.</span><span class="sxs-lookup"><span data-stu-id="37533-207">j.</span></span> <span data-ttu-id="37533-208">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="37533-208">Click **Save**.</span></span>

16. <span data-ttu-id="37533-209">Klik in de klassieke portal van Work.com in het navigatiedeelvenster links op **domeinbeheer** Vouw de bijbehorende sectie en klik vervolgens op **mijn domein** openen de **mijn domein** pagina.</span><span class="sxs-lookup"><span data-stu-id="37533-209">In your Work.com classic portal, on the left navigation pane, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
    
    <span data-ttu-id="37533-210">![Mijn domein](./media/active-directory-saas-work-com-tutorial/ic794115.png "mijn domein")</span><span class="sxs-lookup"><span data-stu-id="37533-210">![My Domain](./media/active-directory-saas-work-com-tutorial/ic794115.png "My Domain")</span></span>

17. <span data-ttu-id="37533-211">Op de **mijn domein** pagina in de **aanmelding pagina huisstijl** sectie, klikt u op **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="37533-211">On the **My Domain** page, in the **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="37533-212">![Aanmeldingspagina huisstijl](./media/active-directory-saas-work-com-tutorial/ic767826.png "aanmeldingspagina huisstijl")</span><span class="sxs-lookup"><span data-stu-id="37533-212">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic767826.png "Login Page Branding")</span></span>

14. <span data-ttu-id="37533-213">Op de **aanmelding pagina huisstijl** pagina in de **verificatieservice** sectie, de naam van uw **SAML SSO instellingen** wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="37533-213">On the **Login Page Branding** page, in the **Authentication Service** section, the name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="37533-214">Selecteer deze en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="37533-214">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="37533-215">![Aanmeldingspagina huisstijl](./media/active-directory-saas-work-com-tutorial/ic784366.png "aanmeldingspagina huisstijl")</span><span class="sxs-lookup"><span data-stu-id="37533-215">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic784366.png "Login Page Branding")</span></span>

> [!TIP]
> <span data-ttu-id="37533-216">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="37533-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="37533-217">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="37533-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="37533-218">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="37533-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="37533-219">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="37533-219">Create an Azure AD test user</span></span>
<span data-ttu-id="37533-220">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="37533-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="37533-222">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="37533-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="37533-223">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="37533-223">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-work-com-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="37533-225">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="37533-225">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Gebruikers en groepen -> alle gebruikers](./media/active-directory-saas-work-com-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="37533-227">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="37533-227">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Toevoegen](./media/active-directory-saas-work-com-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="37533-229">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="37533-229">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Dialoogvenster op de gebruikerspagina](./media/active-directory-saas-work-com-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="37533-231">a.</span><span class="sxs-lookup"><span data-stu-id="37533-231">a.</span></span> <span data-ttu-id="37533-232">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="37533-232">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="37533-233">b.</span><span class="sxs-lookup"><span data-stu-id="37533-233">b.</span></span> <span data-ttu-id="37533-234">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="37533-234">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="37533-235">c.</span><span class="sxs-lookup"><span data-stu-id="37533-235">c.</span></span> <span data-ttu-id="37533-236">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="37533-236">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="37533-237">d.</span><span class="sxs-lookup"><span data-stu-id="37533-237">d.</span></span> <span data-ttu-id="37533-238">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="37533-238">Click **Create**.</span></span>
 
### <a name="create-a-workcom-test-user"></a><span data-ttu-id="37533-239">Een testgebruiker Work.com maken</span><span class="sxs-lookup"><span data-stu-id="37533-239">Create a Work.com test user</span></span>
<span data-ttu-id="37533-240">Voor Azure Active Directory-gebruikers moeten kunnen aanmelden, moeten ze worden ingericht op Work.com.</span><span class="sxs-lookup"><span data-stu-id="37533-240">For Azure Active Directory users to be able to sign in, they must be provisioned to Work.com.</span></span> <span data-ttu-id="37533-241">In het geval van Work.com is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="37533-241">In the case of Work.com, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="37533-242">Als u wilt configureren voor gebruikers inrichten, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="37533-242">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="37533-243">Meld u op met uw bedrijf Work.com site als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="37533-243">Sign on to your Work.com company site as an administrator.</span></span>

2. <span data-ttu-id="37533-244">Ga naar **Setup**.</span><span class="sxs-lookup"><span data-stu-id="37533-244">Go to **Setup**.</span></span>
   
    <span data-ttu-id="37533-245">![Setup](./media/active-directory-saas-work-com-tutorial/IC794108.png "Setup")</span><span class="sxs-lookup"><span data-stu-id="37533-245">![Setup](./media/active-directory-saas-work-com-tutorial/IC794108.png "Setup")</span></span>
3. <span data-ttu-id="37533-246">Ga naar **gebruikers beheren \> gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="37533-246">Go to **Manage Users \> Users**.</span></span>
   
    <span data-ttu-id="37533-247">![Gebruikers beheren](./media/active-directory-saas-work-com-tutorial/IC784369.png "gebruikers beheren")</span><span class="sxs-lookup"><span data-stu-id="37533-247">![Manage Users](./media/active-directory-saas-work-com-tutorial/IC784369.png "Manage Users")</span></span>

4. <span data-ttu-id="37533-248">Klik op **nieuwe gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="37533-248">Click **New User**.</span></span>
   
    <span data-ttu-id="37533-249">![Alle gebruikers](./media/active-directory-saas-work-com-tutorial/IC794117.png "alle gebruikers")</span><span class="sxs-lookup"><span data-stu-id="37533-249">![All Users](./media/active-directory-saas-work-com-tutorial/IC794117.png "All Users")</span></span>

5. <span data-ttu-id="37533-250">Uitvoeren in de sectie gebruikers bewerken in de volgende stappen in de kenmerken van een geldig Azure AD-account die u inrichten in de bijbehorende tekstvakken wilt:</span><span class="sxs-lookup"><span data-stu-id="37533-250">In the User Edit section, perform the following steps, in attributes of a valid Azure AD account you want to provision into the related textboxes:</span></span>
   
    <span data-ttu-id="37533-251">![Gebruiker bewerken](./media/active-directory-saas-work-com-tutorial/ic794118.png "gebruiker bewerken")</span><span class="sxs-lookup"><span data-stu-id="37533-251">![User Edit](./media/active-directory-saas-work-com-tutorial/ic794118.png "User Edit")</span></span>
   
    <span data-ttu-id="37533-252">a.</span><span class="sxs-lookup"><span data-stu-id="37533-252">a.</span></span> <span data-ttu-id="37533-253">In de **voornaam** textbox type de **voornaam** van de gebruiker **Britta**.</span><span class="sxs-lookup"><span data-stu-id="37533-253">In the **First Name** textbox, type the **first name** of the user **Britta**.</span></span>
    
    <span data-ttu-id="37533-254">b.</span><span class="sxs-lookup"><span data-stu-id="37533-254">b.</span></span> <span data-ttu-id="37533-255">In de **achternaam** textbox type de **achternaam** van de gebruiker **Simon**.</span><span class="sxs-lookup"><span data-stu-id="37533-255">In the **Last Name** textbox, type the **last name** of the user **Simon**.</span></span>
    
    <span data-ttu-id="37533-256">c.</span><span class="sxs-lookup"><span data-stu-id="37533-256">c.</span></span> <span data-ttu-id="37533-257">In de **Alias** textbox type de **naam** van de gebruiker **BrittaS**.</span><span class="sxs-lookup"><span data-stu-id="37533-257">In the **Alias** textbox, type the **name** of the user **BrittaS**.</span></span>
    
    <span data-ttu-id="37533-258">d.</span><span class="sxs-lookup"><span data-stu-id="37533-258">d.</span></span> <span data-ttu-id="37533-259">In de **e** textbox type de **e-mailadres** van gebruiker  **Brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="37533-259">In the **Email** textbox, type the **email address** of user **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="37533-260">e.</span><span class="sxs-lookup"><span data-stu-id="37533-260">e.</span></span> <span data-ttu-id="37533-261">In de **gebruikersnaam** textbox, typ een naam van gebruiker, zoals  **Brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="37533-261">In the **User Name** textbox, type a user name of user like **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="37533-262">f.</span><span class="sxs-lookup"><span data-stu-id="37533-262">f.</span></span> <span data-ttu-id="37533-263">In de **bijnaam** textbox, typ een **bijnaam** van gebruiker **Simon**.</span><span class="sxs-lookup"><span data-stu-id="37533-263">In the **Nick Name** textbox, type a **nick name** of user **Simon**.</span></span>
    
    <span data-ttu-id="37533-264">g.</span><span class="sxs-lookup"><span data-stu-id="37533-264">g.</span></span> <span data-ttu-id="37533-265">Selecteer **rol**, **gebruikerslicentie**, en **profiel**.</span><span class="sxs-lookup"><span data-stu-id="37533-265">Select **Role**, **User License**, and **Profile**.</span></span>
    
    <span data-ttu-id="37533-266">h.</span><span class="sxs-lookup"><span data-stu-id="37533-266">h.</span></span> <span data-ttu-id="37533-267">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="37533-267">Click **Save**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="37533-268">De accounthouder Azure AD ontvangt een e-mailbericht met inbegrip van een koppeling om te bevestigen van het account voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="37533-268">The Azure AD account holder will get an email including a link to confirm the account before it becomes active.</span></span>
    > 
    > 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="37533-269">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="37533-269">Assign the Azure AD test user</span></span>

<span data-ttu-id="37533-270">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Work.com.</span><span class="sxs-lookup"><span data-stu-id="37533-270">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Work.com.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="37533-272">**Britta Simon om aan te wijzen Work.com, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="37533-272">**To assign Britta Simon to Work.com, perform the following steps:**</span></span>

1. <span data-ttu-id="37533-273">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="37533-273">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="37533-275">Selecteer in de lijst met toepassingen **Work.com**.</span><span class="sxs-lookup"><span data-stu-id="37533-275">In the applications list, select **Work.com**.</span></span>

    ![Work.com in de lijst van app](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_app.png) 

3. <span data-ttu-id="37533-277">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="37533-277">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="37533-279">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="37533-279">Click **Add** button.</span></span> <span data-ttu-id="37533-280">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="37533-280">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="37533-282">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="37533-282">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="37533-283">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="37533-283">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="37533-284">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="37533-284">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="37533-285">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="37533-285">Test single sign-on</span></span>

<span data-ttu-id="37533-286">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="37533-286">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="37533-287">Als u op de tegel Work.com in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Work.com.</span><span class="sxs-lookup"><span data-stu-id="37533-287">When you click the Work.com tile in the Access Panel, you should get automatically signed-on to your Work.com application.</span></span>
<span data-ttu-id="37533-288">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="37533-288">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="37533-289">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="37533-289">Additional resources</span></span>

* [<span data-ttu-id="37533-290">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="37533-290">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="37533-291">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="37533-291">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_203.png

