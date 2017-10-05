---
title: 'Zelfstudie: Azure Active Directory-integratie met Netsuite | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Netsuite.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dafa0864-aef2-4f5e-9eac-770504688ef4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 4a19ab310212b93a53495a6fc6c25c77dfb82e79
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netsuite"></a><span data-ttu-id="208da-103">Zelfstudie: Azure Active Directory-integratie met Netsuite</span><span class="sxs-lookup"><span data-stu-id="208da-103">Tutorial: Azure Active Directory integration with Netsuite</span></span>

<span data-ttu-id="208da-104">In deze zelfstudie leert u hoe Netsuite integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="208da-104">In this tutorial, you learn how to integrate Netsuite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="208da-105">Netsuite integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="208da-105">Integrating Netsuite with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="208da-106">U kunt beheren in Azure AD die toegang tot Netsuite heeft</span><span class="sxs-lookup"><span data-stu-id="208da-106">You can control in Azure AD who has access to Netsuite</span></span>
- <span data-ttu-id="208da-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Netsuite (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="208da-107">You can enable your users to automatically get signed-on to Netsuite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="208da-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="208da-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="208da-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="208da-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="208da-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="208da-110">Prerequisites</span></span>

<span data-ttu-id="208da-111">Voor het configureren van Azure AD-integratie met Netsuite, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="208da-111">To configure Azure AD integration with Netsuite, you need the following items:</span></span>

- <span data-ttu-id="208da-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="208da-112">An Azure AD subscription</span></span>
- <span data-ttu-id="208da-113">Een Netsuite eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="208da-113">A Netsuite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="208da-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="208da-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="208da-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="208da-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="208da-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="208da-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="208da-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="208da-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="208da-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="208da-118">Scenario description</span></span>
<span data-ttu-id="208da-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="208da-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="208da-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="208da-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="208da-121">Netsuite uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="208da-121">Adding Netsuite from the gallery</span></span>
2. <span data-ttu-id="208da-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="208da-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netsuite-from-the-gallery"></a><span data-ttu-id="208da-123">Netsuite uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="208da-123">Adding Netsuite from the gallery</span></span>
<span data-ttu-id="208da-124">Voor het configureren van de integratie van Netsuite in Azure AD, moet u Netsuite uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="208da-124">To configure the integration of Netsuite into Azure AD, you need to add Netsuite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="208da-125">**Als u wilt toevoegen Netsuite uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="208da-125">**To add Netsuite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="208da-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="208da-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="208da-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="208da-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="208da-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="208da-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="208da-131">Klik op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="208da-131">Click **New application** button on the top of the dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="208da-133">Typ in het zoekvak **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="208da-133">In the search box, type **Netsuite**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_search.png)

5. <span data-ttu-id="208da-135">Selecteer in het deelvenster resultaten **Netsuite**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="208da-135">In the results panel, select **Netsuite**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="208da-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="208da-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="208da-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Netsuite op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="208da-138">In this section, you configure and test Azure AD single sign-on with Netsuite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="208da-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Netsuite is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="208da-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Netsuite is to a user in Azure AD.</span></span> <span data-ttu-id="208da-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Netsuite tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="208da-140">In other words, a link relationship between an Azure AD user and the related user in Netsuite needs to be established.</span></span>

<span data-ttu-id="208da-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Netsuite.</span><span class="sxs-lookup"><span data-stu-id="208da-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Netsuite.</span></span>

<span data-ttu-id="208da-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Netsuite, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="208da-142">To configure and test Azure AD single sign-on with Netsuite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="208da-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="208da-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="208da-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="208da-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="208da-145">**[Maken van een testgebruiker Netsuite](#creating-a-netsuite-test-user)**  - Netsuite die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="208da-145">**[Creating a Netsuite test user](#creating-a-netsuite-test-user)** - to have a counterpart of Britta Simon in Netsuite that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="208da-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="208da-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="208da-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="208da-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="208da-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="208da-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="208da-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Netsuite configureren.</span><span class="sxs-lookup"><span data-stu-id="208da-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Netsuite application.</span></span>

<span data-ttu-id="208da-150">**Voor het configureren van Azure AD eenmalige aanmelding met Netsuite, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="208da-150">**To configure Azure AD single sign-on with Netsuite, perform the following steps:**</span></span>

1. <span data-ttu-id="208da-151">In de Azure-portal op de **Netsuite** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="208da-151">In the Azure portal, on the **Netsuite** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="208da-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="208da-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_samlbase.png)

3. <span data-ttu-id="208da-155">Op de **Netsuite domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="208da-155">On the **Netsuite Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_url.png)

    <span data-ttu-id="208da-157">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen: `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs``https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span><span class="sxs-lookup"><span data-stu-id="208da-157">In the **Reply URL** textbox, type a URL using the following pattern:   `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="208da-158">Deze waarde is geen echte waarde.</span><span class="sxs-lookup"><span data-stu-id="208da-158">This value is not real value.</span></span> <span data-ttu-id="208da-159">Werk de waarde met de werkelijke antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="208da-159">Update the value with the actual Reply URL.</span></span> <span data-ttu-id="208da-160">Neem contact op met [Netsuite ondersteuningsteam](http://www.netsuite.com/portal/services/support.shtml) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="208da-160">Contact [Netsuite support team](http://www.netsuite.com/portal/services/support.shtml) to get this value.</span></span>
 
4. <span data-ttu-id="208da-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="208da-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_certificate.png) 

5. <span data-ttu-id="208da-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="208da-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-netsuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="208da-165">Op de **Netsuite configuratie** sectie, klikt u op **configureren Netsuite** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="208da-165">On the **Netsuite Configuration** section, click **Configure Netsuite** to open **Configure sign-on** window.</span></span> <span data-ttu-id="208da-166">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="208da-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_configure.png) 

7. <span data-ttu-id="208da-168">Een nieuw tabblad openen in uw browser en meld u aan bij uw site van het bedrijf Netsuite als beheerder.</span><span class="sxs-lookup"><span data-stu-id="208da-168">Open a new tab in your browser, and sign into your Netsuite company site as an administrator.</span></span>

8. <span data-ttu-id="208da-169">Klik in de werkbalk boven aan de pagina op **Setup**, klikt u vervolgens op **Installatiebeheer**.</span><span class="sxs-lookup"><span data-stu-id="208da-169">In the toolbar at the top of the page, click **Setup**, then click **Setup Manager**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

9. <span data-ttu-id="208da-171">Van de **instellingstaken** selecteert **integratie**.</span><span class="sxs-lookup"><span data-stu-id="208da-171">From the **Setup Tasks** list, select **Integration**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-integration.png)

10. <span data-ttu-id="208da-173">In de **verificatie beheren** sectie, klikt u op **SAML Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="208da-173">In the **Manage Authentication** section, click **SAML Single Sign-on**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-saml.png)

11. <span data-ttu-id="208da-175">Op de **SAML Setup** pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="208da-175">On the **SAML Setup** page, perform the following steps:</span></span>
   
    <span data-ttu-id="208da-176">a.</span><span class="sxs-lookup"><span data-stu-id="208da-176">a.</span></span> <span data-ttu-id="208da-177">Kopiëren de **SAML Single Sign-On Service-URL** waarde uit de **Naslaggids** sectie van **eenmalige aanmelding configureren** en plak deze in de **identiteit Provider aanmelding Pagina** veld Netsuite.</span><span class="sxs-lookup"><span data-stu-id="208da-177">Copy the **SAML Single Sign-On Service URL** value from **Quick Reference** section of **Configure sign-on** and paste it into the **Identity Provider Login Page** field in Netsuite.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-netsuite-tutorial/ns-saml-setup.png)
  
    <span data-ttu-id="208da-179">b.</span><span class="sxs-lookup"><span data-stu-id="208da-179">b.</span></span> <span data-ttu-id="208da-180">Selecteer in de Netsuite, **primaire methode voor netwerkverificatie**.</span><span class="sxs-lookup"><span data-stu-id="208da-180">In Netsuite, select **Primary Authentication Method**.</span></span>

    <span data-ttu-id="208da-181">c.</span><span class="sxs-lookup"><span data-stu-id="208da-181">c.</span></span> <span data-ttu-id="208da-182">Voor het veld met het label **SAMLV2 identiteit Provider metagegevens**, selecteer **IDP metagegevens-bestand uploaden**.</span><span class="sxs-lookup"><span data-stu-id="208da-182">For the field labeled **SAMLV2 Identity Provider Metadata**, select **Upload IDP Metadata File**.</span></span> <span data-ttu-id="208da-183">Klik vervolgens op **Bladeren** voor het uploaden van het bestand met metagegevens dat u hebt gedownload vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="208da-183">Then click **Browse** to upload the metadata file that you downloaded from Azure portal.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-netsuite-tutorial/ns-sso-setup.png)

    <span data-ttu-id="208da-185">d.</span><span class="sxs-lookup"><span data-stu-id="208da-185">d.</span></span> <span data-ttu-id="208da-186">Klik op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="208da-186">Click **Submit**.</span></span>

12. <span data-ttu-id="208da-187">In Azure AD, klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** selectievakje en het kenmerk toevoegen.</span><span class="sxs-lookup"><span data-stu-id="208da-187">In Azure AD, Click on **View and edit all other user attributes** check-box and add attribute.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-attributes.png)

13. <span data-ttu-id="208da-189">Voor de **kenmerknaam** veld, typt u in `account`.</span><span class="sxs-lookup"><span data-stu-id="208da-189">For the **Attribute Name** field, type in `account`.</span></span> <span data-ttu-id="208da-190">Voor de **kenmerkwaarde** veld, typt u in uw Netsuite account-ID. Deze waarde is constante en wijzigen met account.</span><span class="sxs-lookup"><span data-stu-id="208da-190">For the **Attribute Value** field, type in your Netsuite account ID.This value is constant and change with account.</span></span> <span data-ttu-id="208da-191">Instructies voor het vinden van je account-ID vindt u hieronder:</span><span class="sxs-lookup"><span data-stu-id="208da-191">Instructions on how to find your account ID are included below:</span></span>

      ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-add-attribute.png)

    <span data-ttu-id="208da-193">a.</span><span class="sxs-lookup"><span data-stu-id="208da-193">a.</span></span> <span data-ttu-id="208da-194">Klik in de Netsuite, **Setup** in het menu van de bovenste navigatiebalk.</span><span class="sxs-lookup"><span data-stu-id="208da-194">In Netsuite, click **Setup** from the top navigation menu.</span></span>

    <span data-ttu-id="208da-195">b.</span><span class="sxs-lookup"><span data-stu-id="208da-195">b.</span></span> <span data-ttu-id="208da-196">Klik onder de **instellingstaken** gedeelte van het linkernavigatiegedeelte menu, selecteer de **integratie** sectie en op **Web Services-voorkeuren**.</span><span class="sxs-lookup"><span data-stu-id="208da-196">Then click under the **Setup Tasks** section of the left navigation menu, select the **Integration** section, and click **Web Services Preferences**.</span></span>

    <span data-ttu-id="208da-197">c.</span><span class="sxs-lookup"><span data-stu-id="208da-197">c.</span></span> <span data-ttu-id="208da-198">Uw Account-ID Netsuite Kopieer en plak deze in de **kenmerkwaarde** veld in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="208da-198">Copy your Netsuite Account ID and paste it into the **Attribute Value** field in Azure AD.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-account-id.png)

14. <span data-ttu-id="208da-200">Voordat gebruikers eenmalige aanmelding in Netsuite uitvoeren kunnen, moeten worden ze eerst de juiste machtigingen in Netsuite toegewezen.</span><span class="sxs-lookup"><span data-stu-id="208da-200">Before users can perform single sign-on into Netsuite, they must first be assigned the appropriate permissions in Netsuite.</span></span> <span data-ttu-id="208da-201">Volg de onderstaande instructies om deze machtigingen te wijzen.</span><span class="sxs-lookup"><span data-stu-id="208da-201">Follow the instructions below to assign these permissions.</span></span>

    <span data-ttu-id="208da-202">a.</span><span class="sxs-lookup"><span data-stu-id="208da-202">a.</span></span> <span data-ttu-id="208da-203">Klik op de bovenste navigatiebalk menu **Setup**, klikt u vervolgens op **Installatiebeheer**.</span><span class="sxs-lookup"><span data-stu-id="208da-203">On the top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
      ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="208da-205">b.</span><span class="sxs-lookup"><span data-stu-id="208da-205">b.</span></span> <span data-ttu-id="208da-206">Selecteer in het menu linkernavigatievenster **gebruikers/rollen**, klikt u vervolgens op **rollen beheren**.</span><span class="sxs-lookup"><span data-stu-id="208da-206">On the left navigation menu, select **Users/Roles**, then click **Manage Roles**.</span></span>
      
      ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-manage-roles.png)

    <span data-ttu-id="208da-208">c.</span><span class="sxs-lookup"><span data-stu-id="208da-208">c.</span></span> <span data-ttu-id="208da-209">Klik op **nieuwe rol**.</span><span class="sxs-lookup"><span data-stu-id="208da-209">Click **New Role**.</span></span>

    <span data-ttu-id="208da-210">d.</span><span class="sxs-lookup"><span data-stu-id="208da-210">d.</span></span> <span data-ttu-id="208da-211">Typ in een **naam** voor uw nieuwe rol en selecteer de **eenmalige aanmelding alleen** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="208da-211">Type in a **Name** for your new role, and select the **Single Sign-On Only** checkbox.</span></span>
      
      ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-new-role.png)

    <span data-ttu-id="208da-213">e.</span><span class="sxs-lookup"><span data-stu-id="208da-213">e.</span></span> <span data-ttu-id="208da-214">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="208da-214">Click **Save**.</span></span>

    <span data-ttu-id="208da-215">f.</span><span class="sxs-lookup"><span data-stu-id="208da-215">f.</span></span> <span data-ttu-id="208da-216">Klik in het menu bovenaan op **machtigingen**.</span><span class="sxs-lookup"><span data-stu-id="208da-216">In the menu on the top, click **Permissions**.</span></span> <span data-ttu-id="208da-217">Klik vervolgens op **Setup**.</span><span class="sxs-lookup"><span data-stu-id="208da-217">Then click **Setup**.</span></span>
      
       ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-sso.png)

    <span data-ttu-id="208da-219">g.</span><span class="sxs-lookup"><span data-stu-id="208da-219">g.</span></span> <span data-ttu-id="208da-220">Selecteer **ingesteld Up SAM Single Sign-on**, en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="208da-220">Select **Set Up SAM Single Sign-on**, and then click **Add**.</span></span>

    <span data-ttu-id="208da-221">h.</span><span class="sxs-lookup"><span data-stu-id="208da-221">h.</span></span> <span data-ttu-id="208da-222">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="208da-222">Click **Save**.</span></span>

    <span data-ttu-id="208da-223">ik.</span><span class="sxs-lookup"><span data-stu-id="208da-223">i.</span></span> <span data-ttu-id="208da-224">Klik op de bovenste navigatiebalk menu **Setup**, klikt u vervolgens op **Installatiebeheer**.</span><span class="sxs-lookup"><span data-stu-id="208da-224">On the top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
       ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="208da-226">j.</span><span class="sxs-lookup"><span data-stu-id="208da-226">j.</span></span> <span data-ttu-id="208da-227">Selecteer in het menu linkernavigatievenster **gebruikers/rollen**, klikt u vervolgens op **gebruikers beheren**.</span><span class="sxs-lookup"><span data-stu-id="208da-227">On the left navigation menu, select **Users/Roles**, then click **Manage Users**.</span></span>
      
       ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-manage-users.png)

    <span data-ttu-id="208da-229">k.</span><span class="sxs-lookup"><span data-stu-id="208da-229">k.</span></span> <span data-ttu-id="208da-230">Selecteer een testgebruiker.</span><span class="sxs-lookup"><span data-stu-id="208da-230">Select a test user.</span></span> <span data-ttu-id="208da-231">Klik vervolgens op **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="208da-231">Then click **Edit**.</span></span>
      
       ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-edit-user.png)

    <span data-ttu-id="208da-233">l.</span><span class="sxs-lookup"><span data-stu-id="208da-233">l.</span></span> <span data-ttu-id="208da-234">Selecteer de rol die u hebt gemaakt en klik in het dialoogvenster rollen **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="208da-234">On the Roles dialog, select the role that you have created and click **Add**.</span></span>
      
       ![Eenmalige aanmelding configureren](./media/active-directory-saas-Netsuite-tutorial/ns-add-role.png)

    <span data-ttu-id="208da-236">m.</span><span class="sxs-lookup"><span data-stu-id="208da-236">m.</span></span> <span data-ttu-id="208da-237">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="208da-237">Click **Save**.</span></span>
    
> [!TIP]
> <span data-ttu-id="208da-238">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="208da-238">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="208da-239">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="208da-239">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="208da-240">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="208da-240">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="208da-241">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="208da-241">Creating an Azure AD test user</span></span>
<span data-ttu-id="208da-242">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="208da-242">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="208da-244">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="208da-244">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="208da-245">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="208da-245">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-netsuite-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="208da-247">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="208da-247">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-netsuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="208da-249">Aan de bovenkant van het dialoogvenster, klikt u op **toevoegen** openen de **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="208da-249">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-netsuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="208da-251">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="208da-251">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-netsuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="208da-253">a.</span><span class="sxs-lookup"><span data-stu-id="208da-253">a.</span></span> <span data-ttu-id="208da-254">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="208da-254">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="208da-255">b.</span><span class="sxs-lookup"><span data-stu-id="208da-255">b.</span></span> <span data-ttu-id="208da-256">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="208da-256">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="208da-257">c.</span><span class="sxs-lookup"><span data-stu-id="208da-257">c.</span></span> <span data-ttu-id="208da-258">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="208da-258">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="208da-259">d.</span><span class="sxs-lookup"><span data-stu-id="208da-259">d.</span></span> <span data-ttu-id="208da-260">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="208da-260">Click **Create**.</span></span> 

### <a name="creating-a-netsuite-test-user"></a><span data-ttu-id="208da-261">Een testgebruiker Netsuite maken</span><span class="sxs-lookup"><span data-stu-id="208da-261">Creating a Netsuite test user</span></span>

<span data-ttu-id="208da-262">In deze sectie wordt een gebruiker met de naam Britta Simon gemaakt in Netsuite.</span><span class="sxs-lookup"><span data-stu-id="208da-262">In this section, a user called Britta Simon is created in Netsuite.</span></span> <span data-ttu-id="208da-263">Netsuite ondersteunt just-in-time-inrichting, die standaard is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="208da-263">Netsuite supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="208da-264">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="208da-264">There is no action item for you in this section.</span></span> <span data-ttu-id="208da-265">Als een gebruiker in Netsuite nog niet bestaat, wordt een nieuw gemaakt wanneer u probeert te krijgen tot Netsuite.</span><span class="sxs-lookup"><span data-stu-id="208da-265">If a user doesn't already exist in Netsuite, a new one is created when you attempt to access Netsuite.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="208da-266">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="208da-266">Assigning the Azure AD test user</span></span>

<span data-ttu-id="208da-267">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Netsuite.</span><span class="sxs-lookup"><span data-stu-id="208da-267">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Netsuite.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="208da-269">**Britta Simon om aan te wijzen Netsuite, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="208da-269">**To assign Britta Simon to Netsuite, perform the following steps:**</span></span>

1. <span data-ttu-id="208da-270">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="208da-270">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="208da-272">Selecteer in de lijst met toepassingen **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="208da-272">In the applications list, select **Netsuite**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_app.png) 

3. <span data-ttu-id="208da-274">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="208da-274">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="208da-276">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="208da-276">Click **Add** button.</span></span> <span data-ttu-id="208da-277">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="208da-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="208da-279">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="208da-279">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="208da-280">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="208da-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="208da-281">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="208da-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="208da-282">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="208da-282">Testing single sign-on</span></span>

<span data-ttu-id="208da-283">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="208da-283">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="208da-284">Als u wilt testen van uw instellingen voor eenmalige aanmelding, opent u het toegangsvenster op [https://myapps.microsoft.com](https://myapps.microsoft.com/), meld u aan bij de testaccount en klikt u op **Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="208da-284">To test your single sign-on settings, open the Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), sign into the test account, and click **Netsuite**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="208da-285">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="208da-285">Additional resources</span></span>

* [<span data-ttu-id="208da-286">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="208da-286">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="208da-287">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="208da-287">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="208da-288">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="208da-288">Configure User Provisioning</span></span>](active-directory-saas-netsuite-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_203.png

