---
title: 'Zelfstudie: Azure Active Directory-integratie met TargetProcess | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en TargetProcess.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7cb91628-e758-480d-a233-7a3caaaff50d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: d15931a5d430252bbd9ae342e1f8fde1a539355b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-targetprocess"></a><span data-ttu-id="352c9-103">Zelfstudie: Azure Active Directory-integratie met TargetProcess</span><span class="sxs-lookup"><span data-stu-id="352c9-103">Tutorial: Azure Active Directory integration with TargetProcess</span></span>

<span data-ttu-id="352c9-104">In deze zelfstudie leert u hoe TargetProcess integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="352c9-104">In this tutorial, you learn how to integrate TargetProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="352c9-105">TargetProcess integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="352c9-105">Integrating TargetProcess with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="352c9-106">U kunt beheren in Azure AD die toegang tot TargetProcess heeft</span><span class="sxs-lookup"><span data-stu-id="352c9-106">You can control in Azure AD who has access to TargetProcess</span></span>
- <span data-ttu-id="352c9-107">U kunt uw gebruikers automatisch ophalen aangemeld bij TargetProcess (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="352c9-107">You can enable your users to automatically get signed-on to TargetProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="352c9-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="352c9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="352c9-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="352c9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="352c9-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="352c9-110">Prerequisites</span></span>

<span data-ttu-id="352c9-111">Voor het configureren van Azure AD-integratie met TargetProcess, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="352c9-111">To configure Azure AD integration with TargetProcess, you need the following items:</span></span>

- <span data-ttu-id="352c9-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="352c9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="352c9-113">Een TargetProcess eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="352c9-113">A TargetProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="352c9-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="352c9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="352c9-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="352c9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="352c9-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="352c9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="352c9-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="352c9-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="352c9-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="352c9-118">Scenario description</span></span>
<span data-ttu-id="352c9-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="352c9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="352c9-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="352c9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="352c9-121">TargetProcess uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="352c9-121">Add TargetProcess from the gallery</span></span>
2. <span data-ttu-id="352c9-122">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="352c9-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-targetprocess-from-the-gallery"></a><span data-ttu-id="352c9-123">TargetProcess uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="352c9-123">Add TargetProcess from the gallery</span></span>
<span data-ttu-id="352c9-124">Voor het configureren van de integratie van TargetProcess in Azure AD, moet u TargetProcess uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="352c9-124">To configure the integration of TargetProcess into Azure AD, you need to add TargetProcess from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="352c9-125">**Als u wilt toevoegen TargetProcess uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="352c9-125">**To add TargetProcess from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="352c9-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="352c9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="352c9-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="352c9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="352c9-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="352c9-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="352c9-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="352c9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="352c9-133">Typ in het zoekvak **TargetProcess**, selecteer **TargetProcess** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="352c9-133">In the search box, type **TargetProcess**, select **TargetProcess**  from result panel then click **Add** button to add the application.</span></span>

    ![TargetProcess vanuit galerie toevoegen](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="352c9-135">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="352c9-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="352c9-136">In deze sectie configureert en test eenmalige aanmelding Azure AD met TargetProcess op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="352c9-136">In this section, you configure and test Azure AD single sign-on with TargetProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="352c9-137">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in TargetProcess is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="352c9-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TargetProcess is to a user in Azure AD.</span></span> <span data-ttu-id="352c9-138">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in TargetProcess tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="352c9-138">In other words, a link relationship between an Azure AD user and the related user in TargetProcess needs to be established.</span></span>

<span data-ttu-id="352c9-139">Wijs in TargetProcess, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="352c9-139">In TargetProcess, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="352c9-140">Om te configureren en testen van Azure AD eenmalige aanmelding met TargetProcess, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="352c9-140">To configure and test Azure AD single sign-on with TargetProcess, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="352c9-141">**[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="352c9-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="352c9-142">**[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="352c9-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="352c9-143">**[Maak een testgebruiker TargetProcess](#create-a-targetprocess-test-user)**  - TargetProcess die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="352c9-143">**[Create a TargetProcess test user](#create-a-targetprocess-test-user)** - to have a counterpart of Britta Simon in TargetProcess that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="352c9-144">**[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="352c9-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="352c9-145">**[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="352c9-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="352c9-146">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="352c9-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="352c9-147">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing TargetProcess configureren.</span><span class="sxs-lookup"><span data-stu-id="352c9-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TargetProcess application.</span></span>

<span data-ttu-id="352c9-148">**Voor het configureren van Azure AD eenmalige aanmelding met TargetProcess, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="352c9-148">**To configure Azure AD single sign-on with TargetProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="352c9-149">In de Azure-portal op de **TargetProcess** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="352c9-149">In the Azure portal, on the **TargetProcess** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="352c9-151">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="352c9-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Op basis van SAML eenmalige aanmelding](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_samlbase.png)

3. <span data-ttu-id="352c9-153">Op de **TargetProcess domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="352c9-153">On the **TargetProcess Domain and URLs** section, perform the following steps:</span></span>

    ![Sectie TargetProcess domein en URL 's](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_url.png)

    <span data-ttu-id="352c9-155">a.</span><span class="sxs-lookup"><span data-stu-id="352c9-155">a.</span></span> <span data-ttu-id="352c9-156">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.tpondemand.com/`</span><span class="sxs-lookup"><span data-stu-id="352c9-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.tpondemand.com/`</span></span>

    <span data-ttu-id="352c9-157">b.</span><span class="sxs-lookup"><span data-stu-id="352c9-157">b.</span></span> <span data-ttu-id="352c9-158">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.tpondemand.com/`</span><span class="sxs-lookup"><span data-stu-id="352c9-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.tpondemand.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="352c9-159">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="352c9-159">These values are not real.</span></span> <span data-ttu-id="352c9-160">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="352c9-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="352c9-161">Neem contact op met [TargetProcess Client ondersteuningsteam](mailto:support@targetprocess.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="352c9-161">Contact [TargetProcess Client support team](mailto:support@targetprocess.com) to get these values.</span></span> 
 
4. <span data-ttu-id="352c9-162">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="352c9-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Certificaat voor ondertekening van SAML-sectie](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_certificate.png) 

5. <span data-ttu-id="352c9-164">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="352c9-164">Click **Save** button.</span></span>

    ![knop Opslaan](./media/active-directory-saas-target-process-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="352c9-166">Op de **TargetProcess configuratie** sectie, klikt u op **configureren TargetProcess** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="352c9-166">On the **TargetProcess Configuration** section, click **Configure TargetProcess** to open **Configure sign-on** window.</span></span> <span data-ttu-id="352c9-167">Kopieer de **SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="352c9-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuratiesectie TargetProcess](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_configure.png) 

7. <span data-ttu-id="352c9-169">Eenmalige aanmelding voor uw toepassing TargetProcess als beheerder.</span><span class="sxs-lookup"><span data-stu-id="352c9-169">Sign-on to your TargetProcess application as an administrator.</span></span>

8. <span data-ttu-id="352c9-170">Klik in het menu bovenaan op **Setup**.</span><span class="sxs-lookup"><span data-stu-id="352c9-170">In the menu on the top, click **Setup**.</span></span>
   
    ![Instellen](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_05.png)

9. <span data-ttu-id="352c9-172">Klik op **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="352c9-172">Click **Settings**.</span></span>
   
    ![Instellingen](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_06.png) 

10. <span data-ttu-id="352c9-174">Klik op **Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="352c9-174">Click **Single Sign-on**.</span></span>
   
    ![Klik op eenmalige aanmelding](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_07.png) 

11. <span data-ttu-id="352c9-176">Voer de volgende stappen uit in het dialoogvenster Instellingen voor eenmalige aanmelding:</span><span class="sxs-lookup"><span data-stu-id="352c9-176">On the Single Sign-on settings dialog, perform the following steps:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_08.png)
    
    <span data-ttu-id="352c9-178">a.</span><span class="sxs-lookup"><span data-stu-id="352c9-178">a.</span></span> <span data-ttu-id="352c9-179">Klik op **eenmalige aanmelding inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="352c9-179">Click **Enable Single Sign-on**.</span></span>
    
    <span data-ttu-id="352c9-180">b.</span><span class="sxs-lookup"><span data-stu-id="352c9-180">b.</span></span> <span data-ttu-id="352c9-181">In **aanmeldings-URL** textbox, plak de waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="352c9-181">In **Sign-on URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="352c9-182">c.</span><span class="sxs-lookup"><span data-stu-id="352c9-182">c.</span></span> <span data-ttu-id="352c9-183">Open uw gedownloade certificaat in Kladblok, Kopieer de inhoud en plakt u deze in de **certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="352c9-183">Open your downloaded certificate in notepad, copy the content, and then paste it into the **Certificate** textbox.</span></span>
    
    <span data-ttu-id="352c9-184">d.</span><span class="sxs-lookup"><span data-stu-id="352c9-184">d.</span></span> <span data-ttu-id="352c9-185">Klik op **JIT-inrichting inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="352c9-185">click **Enable JIT Provisioning**.</span></span>

    <span data-ttu-id="352c9-186">e.</span><span class="sxs-lookup"><span data-stu-id="352c9-186">e.</span></span> <span data-ttu-id="352c9-187">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="352c9-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="352c9-188">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="352c9-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="352c9-189">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="352c9-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="352c9-190">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="352c9-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="352c9-191">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="352c9-191">Create an Azure AD test user</span></span>
<span data-ttu-id="352c9-192">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="352c9-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="352c9-194">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="352c9-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="352c9-195">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="352c9-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-target-process-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="352c9-197">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="352c9-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Om de lijst met gebruikers weer te geven](./media/active-directory-saas-target-process-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="352c9-199">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="352c9-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Knop toevoegen](./media/active-directory-saas-target-process-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="352c9-201">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="352c9-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Sectie van de gebruiker](./media/active-directory-saas-target-process-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="352c9-203">a.</span><span class="sxs-lookup"><span data-stu-id="352c9-203">a.</span></span> <span data-ttu-id="352c9-204">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="352c9-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="352c9-205">b.</span><span class="sxs-lookup"><span data-stu-id="352c9-205">b.</span></span> <span data-ttu-id="352c9-206">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="352c9-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="352c9-207">c.</span><span class="sxs-lookup"><span data-stu-id="352c9-207">c.</span></span> <span data-ttu-id="352c9-208">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="352c9-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="352c9-209">d.</span><span class="sxs-lookup"><span data-stu-id="352c9-209">d.</span></span> <span data-ttu-id="352c9-210">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="352c9-210">Click **Create**.</span></span>
 
### <a name="create-a-targetprocess-test-user"></a><span data-ttu-id="352c9-211">Een testgebruiker TargetProcess maken</span><span class="sxs-lookup"><span data-stu-id="352c9-211">Create a TargetProcess test user</span></span>

<span data-ttu-id="352c9-212">Het doel van deze sectie is het maken van een gebruiker Britta Simon in TargetProcess genoemd.</span><span class="sxs-lookup"><span data-stu-id="352c9-212">The objective of this section is to create a user called Britta Simon in TargetProcess.</span></span>

<span data-ttu-id="352c9-213">TargetProcess ondersteuning biedt voor just-in-time-inrichting.</span><span class="sxs-lookup"><span data-stu-id="352c9-213">TargetProcess supports just-in-time provisioning.</span></span> <span data-ttu-id="352c9-214">U hebt al ingeschakeld in [eenmalige aanmelding configureren Azure AD](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="352c9-214">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="352c9-215">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="352c9-215">There is no action item for you in this section.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="352c9-216">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="352c9-216">Assign the Azure AD test user</span></span>

<span data-ttu-id="352c9-217">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="352c9-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TargetProcess.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="352c9-219">**Britta Simon om aan te wijzen TargetProcess, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="352c9-219">**To assign Britta Simon to TargetProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="352c9-220">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="352c9-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="352c9-222">Selecteer in de lijst met toepassingen **TargetProcess**.</span><span class="sxs-lookup"><span data-stu-id="352c9-222">In the applications list, select **TargetProcess**.</span></span>

    ![TargetProcess in lijst met Apps](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_app.png) 

3. <span data-ttu-id="352c9-224">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="352c9-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="352c9-226">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="352c9-226">Click **Add** button.</span></span> <span data-ttu-id="352c9-227">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="352c9-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="352c9-229">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="352c9-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="352c9-230">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="352c9-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="352c9-231">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="352c9-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="352c9-232">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="352c9-232">Test single sign-on</span></span>

<span data-ttu-id="352c9-233">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="352c9-233">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="352c9-234">Als u op de tegel TargetProcess in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="352c9-234">When you click the TargetProcess tile in the Access Panel, you should get automatically signed-on to your TargetProcess application.</span></span> <span data-ttu-id="352c9-235">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="352c9-235">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="352c9-236">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="352c9-236">Additional resources</span></span>

* [<span data-ttu-id="352c9-237">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="352c9-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="352c9-238">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="352c9-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_203.png

