---
title: 'Zelfstudie: Azure Active Directory-integratie met Innotas | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Innotas.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: eb9e9c2c-4b09-4177-bbab-423fd657448e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 674d01b2c0818dc10fdab5844a23c5ebf29bb2d2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-innotas"></a><span data-ttu-id="497b3-103">Zelfstudie: Azure Active Directory-integratie met Innotas</span><span class="sxs-lookup"><span data-stu-id="497b3-103">Tutorial: Azure Active Directory integration with Innotas</span></span>

<span data-ttu-id="497b3-104">In deze zelfstudie leert u hoe Innotas integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="497b3-104">In this tutorial, you learn how to integrate Innotas with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="497b3-105">Innotas integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="497b3-105">Integrating Innotas with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="497b3-106">U kunt beheren in Azure AD die toegang tot Innotas heeft</span><span class="sxs-lookup"><span data-stu-id="497b3-106">You can control in Azure AD who has access to Innotas</span></span>
- <span data-ttu-id="497b3-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Innotas (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="497b3-107">You can enable your users to automatically get signed-on to Innotas (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="497b3-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="497b3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="497b3-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="497b3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="497b3-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="497b3-110">Prerequisites</span></span>

<span data-ttu-id="497b3-111">Voor het configureren van Azure AD-integratie met Innotas, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="497b3-111">To configure Azure AD integration with Innotas, you need the following items:</span></span>

- <span data-ttu-id="497b3-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="497b3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="497b3-113">Een Innotas eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="497b3-113">An Innotas single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="497b3-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="497b3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="497b3-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="497b3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="497b3-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="497b3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="497b3-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="497b3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="497b3-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="497b3-118">Scenario description</span></span>

<span data-ttu-id="497b3-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="497b3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="497b3-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="497b3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="497b3-121">Innotas uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="497b3-121">Adding Innotas from the gallery</span></span>
2. <span data-ttu-id="497b3-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="497b3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-innotas-from-the-gallery"></a><span data-ttu-id="497b3-123">Innotas uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="497b3-123">Adding Innotas from the gallery</span></span>
<span data-ttu-id="497b3-124">Voor het configureren van de integratie van Innotas in Azure AD, moet u Innotas uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="497b3-124">To configure the integration of Innotas into Azure AD, you need to add Innotas from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="497b3-125">**Als u wilt toevoegen Innotas uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="497b3-125">**To add Innotas from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="497b3-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="497b3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="497b3-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="497b3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="497b3-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="497b3-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="497b3-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="497b3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="497b3-133">Typ in het zoekvak **Innotas**.</span><span class="sxs-lookup"><span data-stu-id="497b3-133">In the search box, type **Innotas**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_search.png)

5. <span data-ttu-id="497b3-135">Selecteer in het deelvenster resultaten **Innotas**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="497b3-135">In the results panel, select **Innotas**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="497b3-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="497b3-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="497b3-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Innotas op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="497b3-138">In this section, you configure and test Azure AD single sign-on with Innotas based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="497b3-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Innotas is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="497b3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Innotas is to a user in Azure AD.</span></span> <span data-ttu-id="497b3-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Innotas tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="497b3-140">In other words, a link relationship between an Azure AD user and the related user in Innotas needs to be established.</span></span>

<span data-ttu-id="497b3-141">Wijs in Innotas, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="497b3-141">In Innotas, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="497b3-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Innotas, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="497b3-142">To configure and test Azure AD single sign-on with Innotas, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="497b3-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="497b3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="497b3-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="497b3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="497b3-145">**[Maken van een testgebruiker Innotas](#creating-an-innotas-test-user)**  - Innotas die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="497b3-145">**[Creating an Innotas test user](#creating-an-innotas-test-user)** - to have a counterpart of Britta Simon in Innotas that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="497b3-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="497b3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="497b3-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="497b3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="497b3-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="497b3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="497b3-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Innotas configureren.</span><span class="sxs-lookup"><span data-stu-id="497b3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Innotas application.</span></span>

<span data-ttu-id="497b3-150">**Voor het configureren van Azure AD eenmalige aanmelding met Innotas, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="497b3-150">**To configure Azure AD single sign-on with Innotas, perform the following steps:**</span></span>

1. <span data-ttu-id="497b3-151">In de Azure-portal op de **Innotas** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="497b3-151">In the Azure portal, on the **Innotas** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="497b3-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="497b3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_samlbase.png)

3. <span data-ttu-id="497b3-155">Op de **Innotas domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="497b3-155">On the **Innotas Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_url.png)

    <span data-ttu-id="497b3-157">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<tenant-name>.Innotas.com`</span><span class="sxs-lookup"><span data-stu-id="497b3-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.Innotas.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="497b3-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="497b3-158">This value is not real.</span></span> <span data-ttu-id="497b3-159">Deze waarde bijwerken met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="497b3-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="497b3-160">Neem contact op met [Innotas Client ondersteuningsteam](https://www.innotas.com/contact) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="497b3-160">Contact [Innotas Client support team](https://www.innotas.com/contact) to get this value.</span></span> 
 
4. <span data-ttu-id="497b3-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="497b3-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_certificate.png) 

5. <span data-ttu-id="497b3-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="497b3-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-innotas-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="497b3-165">Eenmalige aanmelding configureren op **Innotas** zijde, moet u de gedownloade verzenden **Metadata XML** naar [Innotas ondersteuningsteam](https://www.innotas.com/contact).</span><span class="sxs-lookup"><span data-stu-id="497b3-165">To configure single sign-on on **Innotas** side, you need to send the downloaded **Metadata XML** to [Innotas support team](https://www.innotas.com/contact).</span></span> <span data-ttu-id="497b3-166">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="497b3-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="497b3-167">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="497b3-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="497b3-168">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="497b3-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="497b3-169">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="497b3-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="497b3-170">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="497b3-170">Creating an Azure AD test user</span></span>

<span data-ttu-id="497b3-171">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="497b3-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="497b3-173">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="497b3-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="497b3-174">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="497b3-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-innotas-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="497b3-176">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="497b3-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-innotas-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="497b3-178">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="497b3-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-innotas-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="497b3-180">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="497b3-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-innotas-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="497b3-182">a.</span><span class="sxs-lookup"><span data-stu-id="497b3-182">a.</span></span> <span data-ttu-id="497b3-183">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="497b3-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="497b3-184">b.</span><span class="sxs-lookup"><span data-stu-id="497b3-184">b.</span></span> <span data-ttu-id="497b3-185">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="497b3-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="497b3-186">c.</span><span class="sxs-lookup"><span data-stu-id="497b3-186">c.</span></span> <span data-ttu-id="497b3-187">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="497b3-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="497b3-188">d.</span><span class="sxs-lookup"><span data-stu-id="497b3-188">d.</span></span> <span data-ttu-id="497b3-189">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="497b3-189">Click **Create**.</span></span>
 
### <a name="creating-an-innotas-test-user"></a><span data-ttu-id="497b3-190">Een testgebruiker Innotas maken</span><span class="sxs-lookup"><span data-stu-id="497b3-190">Creating an Innotas test user</span></span>

<span data-ttu-id="497b3-191">Er is geen actie-item voor gebruikers inrichten voor Innotas configuratie.</span><span class="sxs-lookup"><span data-stu-id="497b3-191">There is no action item for you to configure user provisioning to Innotas.</span></span>  
<span data-ttu-id="497b3-192">Wanneer een toegewezen gebruiker probeert zich aanmelden bij met het toegangsvenster Innotas, Innotas u controleert of de gebruiker bestaat.</span><span class="sxs-lookup"><span data-stu-id="497b3-192">When an assigned user tries to log in to Innotas using the access panel, Innotas checks whether the user exists.</span></span>  

>[!NOTE]
><span data-ttu-id="497b3-193">Als er nog geen gebruikersaccount beschikbaar is, wordt het automatisch gemaakt door Innotas.</span><span class="sxs-lookup"><span data-stu-id="497b3-193">If there is no user account available yet, it is automatically created by Innotas.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="497b3-194">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="497b3-194">Assigning the Azure AD test user</span></span>

<span data-ttu-id="497b3-195">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Innotas.</span><span class="sxs-lookup"><span data-stu-id="497b3-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Innotas.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="497b3-197">**Britta Simon om aan te wijzen Innotas, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="497b3-197">**To assign Britta Simon to Innotas, perform the following steps:**</span></span>

1. <span data-ttu-id="497b3-198">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="497b3-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="497b3-200">Selecteer in de lijst met toepassingen **Innotas**.</span><span class="sxs-lookup"><span data-stu-id="497b3-200">In the applications list, select **Innotas**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_app.png) 

3. <span data-ttu-id="497b3-202">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="497b3-202">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="497b3-204">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="497b3-204">Click **Add** button.</span></span> <span data-ttu-id="497b3-205">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="497b3-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="497b3-207">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="497b3-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="497b3-208">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="497b3-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="497b3-209">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="497b3-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="497b3-210">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="497b3-210">Testing single sign-on</span></span>

<span data-ttu-id="497b3-211">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="497b3-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="497b3-212">Als u op de tegel Innotas in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing Innotas.</span><span class="sxs-lookup"><span data-stu-id="497b3-212">When you click the Innotas tile in the Access Panel, you should get automatically signed-on to your Innotas application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="497b3-213">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="497b3-213">Additional resources</span></span>

* [<span data-ttu-id="497b3-214">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="497b3-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="497b3-215">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="497b3-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_203.png

