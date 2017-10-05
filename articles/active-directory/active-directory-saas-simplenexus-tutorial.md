---
title: 'Zelfstudie: Azure Active Directory-integratie met SimpleNexus | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en SimpleNexus.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 89821a05-88e2-4579-b144-0123b2b9cb95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: bddd82b986039cf67827cb407f500edb2000964b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-simplenexus"></a><span data-ttu-id="8a982-103">Zelfstudie: Azure Active Directory-integratie met SimpleNexus</span><span class="sxs-lookup"><span data-stu-id="8a982-103">Tutorial: Azure Active Directory integration with SimpleNexus</span></span>

<span data-ttu-id="8a982-104">In deze zelfstudie leert u hoe SimpleNexus integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8a982-104">In this tutorial, you learn how to integrate SimpleNexus with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8a982-105">SimpleNexus integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="8a982-105">Integrating SimpleNexus with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8a982-106">U kunt beheren in Azure AD die toegang tot SimpleNexus heeft</span><span class="sxs-lookup"><span data-stu-id="8a982-106">You can control in Azure AD who has access to SimpleNexus</span></span>
- <span data-ttu-id="8a982-107">U kunt uw gebruikers automatisch ophalen aangemeld bij SimpleNexus (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="8a982-107">You can enable your users to automatically get signed-on to SimpleNexus (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8a982-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="8a982-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8a982-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8a982-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a982-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8a982-110">Prerequisites</span></span>

<span data-ttu-id="8a982-111">Voor het configureren van Azure AD-integratie met SimpleNexus, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="8a982-111">To configure Azure AD integration with SimpleNexus, you need the following items:</span></span>

- <span data-ttu-id="8a982-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="8a982-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8a982-113">Een SimpleNexus eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="8a982-113">A SimpleNexus single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8a982-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="8a982-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8a982-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="8a982-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8a982-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="8a982-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8a982-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8a982-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8a982-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="8a982-118">Scenario description</span></span>
<span data-ttu-id="8a982-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="8a982-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8a982-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="8a982-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8a982-121">SimpleNexus uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="8a982-121">Adding SimpleNexus from the gallery</span></span>
2. <span data-ttu-id="8a982-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="8a982-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-simplenexus-from-the-gallery"></a><span data-ttu-id="8a982-123">SimpleNexus uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="8a982-123">Adding SimpleNexus from the gallery</span></span>
<span data-ttu-id="8a982-124">Voor het configureren van de integratie van SimpleNexus in Azure AD, moet u SimpleNexus uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="8a982-124">To configure the integration of SimpleNexus into Azure AD, you need to add SimpleNexus from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8a982-125">**Als u wilt toevoegen SimpleNexus uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="8a982-125">**To add SimpleNexus from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8a982-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="8a982-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8a982-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8a982-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8a982-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8a982-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="8a982-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8a982-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="8a982-133">Typ in het zoekvak **SimpleNexus**.</span><span class="sxs-lookup"><span data-stu-id="8a982-133">In the search box, type **SimpleNexus**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_search.png)

5. <span data-ttu-id="8a982-135">Selecteer in het deelvenster resultaten **SimpleNexus**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="8a982-135">In the results panel, select **SimpleNexus**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8a982-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="8a982-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8a982-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met SimpleNexus op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="8a982-138">In this section, you configure and test Azure AD single sign-on with SimpleNexus based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8a982-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in SimpleNexus is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8a982-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SimpleNexus is to a user in Azure AD.</span></span> <span data-ttu-id="8a982-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in SimpleNexus tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="8a982-140">In other words, a link relationship between an Azure AD user and the related user in SimpleNexus needs to be established.</span></span>

<span data-ttu-id="8a982-141">Wijs in SimpleNexus, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="8a982-141">In SimpleNexus, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8a982-142">Om te configureren en testen van Azure AD eenmalige aanmelding met SimpleNexus, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="8a982-142">To configure and test Azure AD single sign-on with SimpleNexus, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8a982-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8a982-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8a982-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8a982-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8a982-145">**[Maken van een testgebruiker SimpleNexus](#creating-a-simplenexus-test-user)**  - SimpleNexus die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="8a982-145">**[Creating a SimpleNexus test user](#creating-a-simplenexus-test-user)** - to have a counterpart of Britta Simon in SimpleNexus that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8a982-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="8a982-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8a982-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="8a982-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8a982-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="8a982-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8a982-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing SimpleNexus configureren.</span><span class="sxs-lookup"><span data-stu-id="8a982-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SimpleNexus application.</span></span>

<span data-ttu-id="8a982-150">**Voor het configureren van Azure AD eenmalige aanmelding met SimpleNexus, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="8a982-150">**To configure Azure AD single sign-on with SimpleNexus, perform the following steps:**</span></span>

1. <span data-ttu-id="8a982-151">In de Azure-portal op de **SimpleNexus** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="8a982-151">In the Azure portal, on the **SimpleNexus** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="8a982-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="8a982-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_samlbase.png)

3. <span data-ttu-id="8a982-155">Op de **SimpleNexus domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="8a982-155">On the **SimpleNexus Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_url.png)

    <span data-ttu-id="8a982-157">a.</span><span class="sxs-lookup"><span data-stu-id="8a982-157">a.</span></span> <span data-ttu-id="8a982-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://simplenexus.com/<companyname>_login`</span><span class="sxs-lookup"><span data-stu-id="8a982-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://simplenexus.com/<companyname>_login`</span></span>

    <span data-ttu-id="8a982-159">b.</span><span class="sxs-lookup"><span data-stu-id="8a982-159">b.</span></span> <span data-ttu-id="8a982-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://simplenexus.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="8a982-160">In the **Identifier** textbox, type a URL using the following pattern: `https://simplenexus.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8a982-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="8a982-161">These values are not real.</span></span> <span data-ttu-id="8a982-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="8a982-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8a982-163">Neem contact op met [SimpleNexus Client ondersteuningsteam](https://simplenexus.com/site/contact) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="8a982-163">Contact [SimpleNexus Client support team](https://simplenexus.com/site/contact) to get these values.</span></span> 
 
4. <span data-ttu-id="8a982-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="8a982-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_certificate.png) 

5. <span data-ttu-id="8a982-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="8a982-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-simplenexus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8a982-168">Eenmalige aanmelding configureren op **SimpleNexus** zijde, moet u de gedownloade verzenden **Metadata XML** naar [SimpleNexus ondersteuningsteam](https://simplenexus.com/site/contact).</span><span class="sxs-lookup"><span data-stu-id="8a982-168">To configure single sign-on on **SimpleNexus** side, you need to send the downloaded **Metadata XML** to [SimpleNexus support team](https://simplenexus.com/site/contact).</span></span> <span data-ttu-id="8a982-169">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="8a982-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="8a982-170">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="8a982-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8a982-171">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="8a982-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8a982-172">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8a982-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8a982-173">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="8a982-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="8a982-174">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="8a982-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="8a982-176">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="8a982-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8a982-177">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="8a982-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-simplenexus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8a982-179">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="8a982-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-simplenexus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8a982-181">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8a982-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-simplenexus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8a982-183">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="8a982-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-simplenexus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8a982-185">a.</span><span class="sxs-lookup"><span data-stu-id="8a982-185">a.</span></span> <span data-ttu-id="8a982-186">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8a982-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8a982-187">b.</span><span class="sxs-lookup"><span data-stu-id="8a982-187">b.</span></span> <span data-ttu-id="8a982-188">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8a982-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8a982-189">c.</span><span class="sxs-lookup"><span data-stu-id="8a982-189">c.</span></span> <span data-ttu-id="8a982-190">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="8a982-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8a982-191">d.</span><span class="sxs-lookup"><span data-stu-id="8a982-191">d.</span></span> <span data-ttu-id="8a982-192">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="8a982-192">Click **Create**.</span></span>
 
### <a name="creating-a-simplenexus-test-user"></a><span data-ttu-id="8a982-193">Een testgebruiker SimpleNexus maken</span><span class="sxs-lookup"><span data-stu-id="8a982-193">Creating a SimpleNexus test user</span></span>

<span data-ttu-id="8a982-194">Om Azure AD-gebruikers zich aanmelden bij SimpleNexus inschakelt, moeten ze worden ingericht in SimpleNexus.</span><span class="sxs-lookup"><span data-stu-id="8a982-194">In order to enable Azure AD users to log in to SimpleNexus, they must be provisioned into SimpleNexus.</span></span>

<span data-ttu-id="8a982-195">In het geval van SimpleNexus is inrichting een handmatige taak uitgevoerd door de tenantbeheerder.</span><span class="sxs-lookup"><span data-stu-id="8a982-195">In the case of SimpleNexus, provisioning is a manual task performed by the tenant administrator.</span></span>

>[!NOTE]
><span data-ttu-id="8a982-196">U kunt andere SimpleNexus gebruiker account hulpmiddelen voor het maken of API's die is geleverd door SimpleNexus aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="8a982-196">You can use any other SimpleNexus user account creation tools or APIs provided by SimpleNexus to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8a982-197">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a982-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8a982-198">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan SimpleNexus.</span><span class="sxs-lookup"><span data-stu-id="8a982-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SimpleNexus.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="8a982-200">**Britta Simon om aan te wijzen SimpleNexus, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="8a982-200">**To assign Britta Simon to SimpleNexus, perform the following steps:**</span></span>

1. <span data-ttu-id="8a982-201">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8a982-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="8a982-203">Selecteer in de lijst met toepassingen **SimpleNexus**.</span><span class="sxs-lookup"><span data-stu-id="8a982-203">In the applications list, select **SimpleNexus**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_app.png) 

3. <span data-ttu-id="8a982-205">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="8a982-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="8a982-207">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="8a982-207">Click **Add** button.</span></span> <span data-ttu-id="8a982-208">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8a982-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="8a982-210">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="8a982-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8a982-211">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8a982-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8a982-212">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8a982-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8a982-213">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="8a982-213">Testing single sign-on</span></span>

<span data-ttu-id="8a982-214">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="8a982-214">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8a982-215">Als u op de tegel SimpleNexus in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing SimpleNexus.</span><span class="sxs-lookup"><span data-stu-id="8a982-215">When you click the SimpleNexus tile in the Access Panel, you should get automatically signed-on to your SimpleNexus application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8a982-216">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="8a982-216">Additional resources</span></span>

* [<span data-ttu-id="8a982-217">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8a982-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8a982-218">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8a982-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_203.png

