---
title: 'Zelfstudie: Azure Active Directory-integratie met Lynda.com | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Lynda.com.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6c92789-8b64-4049-bac9-8cb928398433
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: 84ed2adcc2d49ddbb6bd2e9cc3b93b967ebed063
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lyndacom"></a><span data-ttu-id="da1b0-103">Zelfstudie: Azure Active Directory-integratie met Lynda.com</span><span class="sxs-lookup"><span data-stu-id="da1b0-103">Tutorial: Azure Active Directory integration with Lynda.com</span></span>

<span data-ttu-id="da1b0-104">In deze zelfstudie leert u hoe Lynda.com integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="da1b0-104">In this tutorial, you learn how to integrate Lynda.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="da1b0-105">Lynda.com integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="da1b0-105">Integrating Lynda.com with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="da1b0-106">U kunt beheren in Azure AD die toegang tot Lynda.com heeft</span><span class="sxs-lookup"><span data-stu-id="da1b0-106">You can control in Azure AD who has access to Lynda.com</span></span>
- <span data-ttu-id="da1b0-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Lynda.com (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="da1b0-107">You can enable your users to automatically get signed-on to Lynda.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="da1b0-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="da1b0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="da1b0-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="da1b0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="da1b0-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="da1b0-110">Prerequisites</span></span>

<span data-ttu-id="da1b0-111">Voor het configureren van Azure AD-integratie met Lynda.com, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="da1b0-111">To configure Azure AD integration with Lynda.com, you need the following items:</span></span>

- <span data-ttu-id="da1b0-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="da1b0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="da1b0-113">Een Lynda.com eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="da1b0-113">A Lynda.com single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="da1b0-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="da1b0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="da1b0-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="da1b0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="da1b0-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="da1b0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="da1b0-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="da1b0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="da1b0-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="da1b0-118">Scenario description</span></span>
<span data-ttu-id="da1b0-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="da1b0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="da1b0-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="da1b0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="da1b0-121">Lynda.com uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="da1b0-121">Adding Lynda.com from the gallery</span></span>
2. <span data-ttu-id="da1b0-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="da1b0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lyndacom-from-the-gallery"></a><span data-ttu-id="da1b0-123">Lynda.com uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="da1b0-123">Adding Lynda.com from the gallery</span></span>
<span data-ttu-id="da1b0-124">Voor het configureren van de integratie van Lynda.com in Azure AD, moet u Lynda.com uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="da1b0-124">To configure the integration of Lynda.com into Azure AD, you need to add Lynda.com from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="da1b0-125">**Als u wilt toevoegen Lynda.com uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="da1b0-125">**To add Lynda.com from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="da1b0-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="da1b0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="da1b0-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="da1b0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="da1b0-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="da1b0-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="da1b0-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="da1b0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="da1b0-133">Typ in het zoekvak **Lynda.com**.</span><span class="sxs-lookup"><span data-stu-id="da1b0-133">In the search box, type **Lynda.com**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_search.png)

5. <span data-ttu-id="da1b0-135">Selecteer in het deelvenster resultaten **Lynda.com**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="da1b0-135">In the results panel, select **Lynda.com**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="da1b0-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="da1b0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="da1b0-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Lynda.com op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="da1b0-138">In this section, you configure and test Azure AD single sign-on with Lynda.com based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="da1b0-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Lynda.com is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="da1b0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lynda.com is to a user in Azure AD.</span></span> <span data-ttu-id="da1b0-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Lynda.com tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="da1b0-140">In other words, a link relationship between an Azure AD user and the related user in Lynda.com needs to be established.</span></span>

<span data-ttu-id="da1b0-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="da1b0-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Lynda.com.</span></span>

<span data-ttu-id="da1b0-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Lynda.com, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="da1b0-142">To configure and test Azure AD single sign-on with Lynda.com, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="da1b0-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="da1b0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="da1b0-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="da1b0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="da1b0-145">**[Maken van een testgebruiker Lynda.com](#creating-a-lyndacom-test-user)**  - Lynda.com die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="da1b0-145">**[Creating a Lynda.com test user](#creating-a-lyndacom-test-user)** - to have a counterpart of Britta Simon in Lynda.com that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="da1b0-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="da1b0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="da1b0-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="da1b0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="da1b0-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="da1b0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="da1b0-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Lynda.com configureren.</span><span class="sxs-lookup"><span data-stu-id="da1b0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lynda.com application.</span></span>

<span data-ttu-id="da1b0-150">**Voor het configureren van Azure AD eenmalige aanmelding met Lynda.com, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="da1b0-150">**To configure Azure AD single sign-on with Lynda.com, perform the following steps:**</span></span>

1. <span data-ttu-id="da1b0-151">In de Azure-portal op de **Lynda.com** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="da1b0-151">In the Azure portal, on the **Lynda.com** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="da1b0-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="da1b0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_samlbase.png)

3. <span data-ttu-id="da1b0-155">Op de **Lynda.com domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="da1b0-155">On the **Lynda.com Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_url.png)

    <span data-ttu-id="da1b0-157">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `</span><span class="sxs-lookup"><span data-stu-id="da1b0-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `</span></span>

    > [!NOTE] 
    > <span data-ttu-id="da1b0-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="da1b0-158">This value is not real.</span></span> <span data-ttu-id="da1b0-159">Deze waarde bijwerken met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="da1b0-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="da1b0-160">Neem contact op met [Lynda.com Client ondersteuningsteam](https://www.linkedin.com/help/lynda/ask) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="da1b0-160">Contact [Lynda.com Client support team](https://www.linkedin.com/help/lynda/ask) to get these values.</span></span> 
 
4. <span data-ttu-id="da1b0-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="da1b0-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_certificate.png) 

5. <span data-ttu-id="da1b0-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="da1b0-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lynda-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="da1b0-165">Eenmalige aanmelding configureren op **Lynda.com** zijde, moet u de gedownloade verzenden **Metadata XML** [Lynda.com ondersteuning](https://www.linkedin.com/help/lynda/ask).</span><span class="sxs-lookup"><span data-stu-id="da1b0-165">To configure single sign-on on **Lynda.com** side, you need to send the downloaded **Metadata XML** [Lynda.com support](https://www.linkedin.com/help/lynda/ask).</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="da1b0-166">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="da1b0-166">Creating an Azure AD test user</span></span>
<span data-ttu-id="da1b0-167">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="da1b0-167">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="da1b0-169">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="da1b0-169">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="da1b0-170">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="da1b0-170">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lynda-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="da1b0-172">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="da1b0-172">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lynda-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="da1b0-174">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="da1b0-174">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lynda-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="da1b0-176">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="da1b0-176">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-lynda-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="da1b0-178">a.</span><span class="sxs-lookup"><span data-stu-id="da1b0-178">a.</span></span> <span data-ttu-id="da1b0-179">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="da1b0-179">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="da1b0-180">b.</span><span class="sxs-lookup"><span data-stu-id="da1b0-180">b.</span></span> <span data-ttu-id="da1b0-181">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="da1b0-181">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="da1b0-182">c.</span><span class="sxs-lookup"><span data-stu-id="da1b0-182">c.</span></span> <span data-ttu-id="da1b0-183">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="da1b0-183">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="da1b0-184">d.</span><span class="sxs-lookup"><span data-stu-id="da1b0-184">d.</span></span> <span data-ttu-id="da1b0-185">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="da1b0-185">Click **Create**.</span></span>
 
### <a name="creating-a-lyndacom-test-user"></a><span data-ttu-id="da1b0-186">Een testgebruiker Lynda.com maken</span><span class="sxs-lookup"><span data-stu-id="da1b0-186">Creating a Lynda.com test user</span></span>

<span data-ttu-id="da1b0-187">Er is geen actie-item voor gebruikers inrichten voor Lynda.com configuratie.</span><span class="sxs-lookup"><span data-stu-id="da1b0-187">There is no action item for you to configure user provisioning to Lynda.com.</span></span>  
<span data-ttu-id="da1b0-188">Wanneer een toegewezen gebruiker probeert zich aanmelden bij met het toegangsvenster Lynda.com, Lynda.com u controleert of de gebruiker bestaat.</span><span class="sxs-lookup"><span data-stu-id="da1b0-188">When an assigned user tries to log in to Lynda.com using the access panel, Lynda.com checks whether the user exists.</span></span>  

<span data-ttu-id="da1b0-189">Als er nog geen gebruikersaccount beschikbaar is, wordt het automatisch gemaakt door Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="da1b0-189">If there is no user account available yet, it is automatically created by Lynda.com.</span></span>

>[!NOTE]
><span data-ttu-id="da1b0-190">U kunt andere Lynda.com gebruiker account hulpmiddelen voor het maken of API's die is geleverd door Lynda.com aan inrichten AAD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="da1b0-190">You can use any other Lynda.com user account creation tools or APIs provided by Lynda.com to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="da1b0-191">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="da1b0-191">Assigning the Azure AD test user</span></span>

<span data-ttu-id="da1b0-192">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="da1b0-192">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lynda.com.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="da1b0-194">**Britta Simon om aan te wijzen Lynda.com, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="da1b0-194">**To assign Britta Simon to Lynda.com, perform the following steps:**</span></span>

1. <span data-ttu-id="da1b0-195">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="da1b0-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="da1b0-197">Selecteer in de lijst met toepassingen **Lynda.com**.</span><span class="sxs-lookup"><span data-stu-id="da1b0-197">In the applications list, select **Lynda.com**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_app.png) 

3. <span data-ttu-id="da1b0-199">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="da1b0-199">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="da1b0-201">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="da1b0-201">Click **Add** button.</span></span> <span data-ttu-id="da1b0-202">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="da1b0-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="da1b0-204">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="da1b0-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="da1b0-205">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="da1b0-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="da1b0-206">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="da1b0-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="da1b0-207">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="da1b0-207">Testing single sign-on</span></span>

<span data-ttu-id="da1b0-208">Als u testen van uw instellingen voor eenmalige aanmelding wilt, opent u het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="da1b0-208">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="da1b0-209">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="da1b0-209">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="da1b0-210">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="da1b0-210">Additional resources</span></span>

* [<span data-ttu-id="da1b0-211">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="da1b0-211">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="da1b0-212">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="da1b0-212">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_203.png

