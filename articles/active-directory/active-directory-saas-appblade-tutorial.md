---
title: 'Zelfstudie: Azure Active Directory-integratie met AppBlade | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en AppBlade.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3360d7aa-6518-4f99-88bd-b7f7258183e8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 7820a70b34b6d25ba81b17c472159d08904335d1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-appblade"></a><span data-ttu-id="680d2-103">Zelfstudie: Azure Active Directory-integratie met AppBlade</span><span class="sxs-lookup"><span data-stu-id="680d2-103">Tutorial: Azure Active Directory integration with AppBlade</span></span>

<span data-ttu-id="680d2-104">In deze zelfstudie leert u hoe AppBlade integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="680d2-104">In this tutorial, you learn how to integrate AppBlade with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="680d2-105">AppBlade integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="680d2-105">Integrating AppBlade with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="680d2-106">U kunt beheren in Azure AD die toegang tot AppBlade heeft</span><span class="sxs-lookup"><span data-stu-id="680d2-106">You can control in Azure AD who has access to AppBlade</span></span>
- <span data-ttu-id="680d2-107">U kunt uw gebruikers automatisch ophalen aangemeld bij AppBlade (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="680d2-107">You can enable your users to automatically get signed-on to AppBlade (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="680d2-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="680d2-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="680d2-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="680d2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="680d2-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="680d2-110">Prerequisites</span></span>

<span data-ttu-id="680d2-111">Voor het configureren van Azure AD-integratie met AppBlade, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="680d2-111">To configure Azure AD integration with AppBlade, you need the following items:</span></span>

- <span data-ttu-id="680d2-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="680d2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="680d2-113">Een AppBlade eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="680d2-113">An AppBlade single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="680d2-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="680d2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="680d2-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="680d2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="680d2-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="680d2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="680d2-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="680d2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="680d2-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="680d2-118">Scenario description</span></span>
<span data-ttu-id="680d2-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="680d2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="680d2-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="680d2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="680d2-121">AppBlade uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="680d2-121">Adding AppBlade from the gallery</span></span>
2. <span data-ttu-id="680d2-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="680d2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-appblade-from-the-gallery"></a><span data-ttu-id="680d2-123">AppBlade uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="680d2-123">Adding AppBlade from the gallery</span></span>
<span data-ttu-id="680d2-124">Voor het configureren van de integratie van AppBlade in Azure AD, moet u AppBlade uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="680d2-124">To configure the integration of AppBlade into Azure AD, you need to add AppBlade from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="680d2-125">**Als u wilt toevoegen AppBlade uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="680d2-125">**To add AppBlade from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="680d2-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="680d2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="680d2-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="680d2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="680d2-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="680d2-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="680d2-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="680d2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="680d2-133">Typ in het zoekvak **AppBlade**.</span><span class="sxs-lookup"><span data-stu-id="680d2-133">In the search box, type **AppBlade**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_search.png)

5. <span data-ttu-id="680d2-135">Selecteer in het deelvenster resultaten **AppBlade**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="680d2-135">In the results panel, select **AppBlade**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="680d2-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="680d2-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="680d2-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met AppBlade op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="680d2-138">In this section, you configure and test Azure AD single sign-on with AppBlade based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="680d2-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in AppBlade is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="680d2-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AppBlade is to a user in Azure AD.</span></span> <span data-ttu-id="680d2-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in AppBlade tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="680d2-140">In other words, a link relationship between an Azure AD user and the related user in AppBlade needs to be established.</span></span>

<span data-ttu-id="680d2-141">Wijs in AppBlade, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="680d2-141">In AppBlade, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="680d2-142">Om te configureren en testen van Azure AD eenmalige aanmelding met AppBlade, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="680d2-142">To configure and test Azure AD single sign-on with AppBlade, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="680d2-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="680d2-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="680d2-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="680d2-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="680d2-145">**[Maken van een testgebruiker AppBlade](#creating-an-appblade-test-user)**  - AppBlade die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="680d2-145">**[Creating an AppBlade test user](#creating-an-appblade-test-user)** - to have a counterpart of Britta Simon in AppBlade that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="680d2-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="680d2-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="680d2-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="680d2-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="680d2-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="680d2-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="680d2-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing AppBlade configureren.</span><span class="sxs-lookup"><span data-stu-id="680d2-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AppBlade application.</span></span>

<span data-ttu-id="680d2-150">**Voor het configureren van Azure AD eenmalige aanmelding met AppBlade, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="680d2-150">**To configure Azure AD single sign-on with AppBlade, perform the following steps:**</span></span>

1. <span data-ttu-id="680d2-151">In de Azure-portal op de **AppBlade** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="680d2-151">In the Azure portal, on the **AppBlade** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="680d2-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="680d2-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_samlbase.png)

3. <span data-ttu-id="680d2-155">Op de **AppBlade domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="680d2-155">On the **AppBlade Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_url.png)

    <span data-ttu-id="680d2-157">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.appblade.com/saml/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="680d2-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.appblade.com/saml/<tenantid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="680d2-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="680d2-158">This value is not real.</span></span> <span data-ttu-id="680d2-159">Werk de waarde met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="680d2-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="680d2-160">Neem contact op met [AppBlade Client ondersteuningsteam](mailto:support@appblade.com) de waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="680d2-160">Contact [AppBlade Client support team](mailto:support@appblade.com) to get the value.</span></span> 
 
4. <span data-ttu-id="680d2-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="680d2-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_certificate.png) 

5. <span data-ttu-id="680d2-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="680d2-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-appblade-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="680d2-165">Eenmalige aanmelding configureren op **AppBlade** zijde, moet u de gedownloade verzenden **Metadata XML** naar [AppBlade ondersteuningsteam](mailto:support@appblade.com).</span><span class="sxs-lookup"><span data-stu-id="680d2-165">To configure single sign-on on **AppBlade** side, you need to send the downloaded **Metadata XML** to [AppBlade support team](mailto:support@appblade.com).</span></span> <span data-ttu-id="680d2-166">Verder vraag ze voor het configureren van de **URL SSO-verlener** als `https://appblade.com/saml`.</span><span class="sxs-lookup"><span data-stu-id="680d2-166">Also, please ask them to configure the **SSO Issuer URL** as `https://appblade.com/saml`.</span></span> <span data-ttu-id="680d2-167">Deze instelling is vereist voor eenmalige aanmelding werkt.</span><span class="sxs-lookup"><span data-stu-id="680d2-167">This setting is required for single sign-on to work.</span></span>


> [!TIP]
> <span data-ttu-id="680d2-168">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="680d2-168">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="680d2-169">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="680d2-169">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="680d2-170">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="680d2-170">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="680d2-171">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="680d2-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="680d2-172">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="680d2-172">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="680d2-174">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="680d2-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="680d2-175">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="680d2-175">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-appblade-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="680d2-177">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="680d2-177">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-appblade-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="680d2-179">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="680d2-179">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-appblade-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="680d2-181">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="680d2-181">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-appblade-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="680d2-183">a.</span><span class="sxs-lookup"><span data-stu-id="680d2-183">a.</span></span> <span data-ttu-id="680d2-184">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="680d2-184">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="680d2-185">b.</span><span class="sxs-lookup"><span data-stu-id="680d2-185">b.</span></span> <span data-ttu-id="680d2-186">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="680d2-186">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="680d2-187">c.</span><span class="sxs-lookup"><span data-stu-id="680d2-187">c.</span></span> <span data-ttu-id="680d2-188">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="680d2-188">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="680d2-189">d.</span><span class="sxs-lookup"><span data-stu-id="680d2-189">d.</span></span> <span data-ttu-id="680d2-190">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="680d2-190">Click **Create**.</span></span>
 
### <a name="creating-an-appblade-test-user"></a><span data-ttu-id="680d2-191">Een testgebruiker AppBlade maken</span><span class="sxs-lookup"><span data-stu-id="680d2-191">Creating an AppBlade test user</span></span>

<span data-ttu-id="680d2-192">Het doel van deze sectie is het maken van een gebruiker Britta Simon in AppBlade genoemd.</span><span class="sxs-lookup"><span data-stu-id="680d2-192">The objective of this section is to create a user called Britta Simon in AppBlade.</span></span> <span data-ttu-id="680d2-193">AppBlade ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="680d2-193">AppBlade supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="680d2-194">**Zorg ervoor dat de domeinnaam van uw is geconfigureerd met AppBlade voor gebruikers inrichten. Inrichting werkt nadat dat alleen de just-in-time-gebruiker.**</span><span class="sxs-lookup"><span data-stu-id="680d2-194">**Make sure that your domain name is configured with AppBlade for user provisioning. After that only the just-in-time user provisioning works.**</span></span>

<span data-ttu-id="680d2-195">Als de gebruiker een e-mailadres dat eindigt met het domein dat is geconfigureerd door AppBlade voor uw account en vervolgens de gebruiker wordt automatisch het account toegevoegd als een lid met het machtigingsniveau die u opgeeft heeft, dit is een 'Basic' (een basic gebruiker die u kunt toepassingen alleen installeren) , 'Teamlid' (een gebruiker die u kunt nieuwe versies van de app uploaden en beheren van de projecten) of 'Administrator' (volledig Administrator-bevoegdheden aan het account).</span><span class="sxs-lookup"><span data-stu-id="680d2-195">If the user has an email address ending with the domain configured by AppBlade for your account, then the user will automatically join the account as a member with the permission level you specify, which is one of "Basic" (a basic user who can only install applications), "Team Member" (a user who can upload new app versions and manage projects), or "Administrator" (full admin privileges to the account).</span></span> <span data-ttu-id="680d2-196">Normaal zou een Basic kiezen en vervolgens promoveren gebruikers handmatig via een aanmeldgegevens van serverbeheerder (AppBlade moet een op basis van e-beheerderaanmelding vooraf configureren of het promoveren van een gebruiker namens de klant na aanmelding).</span><span class="sxs-lookup"><span data-stu-id="680d2-196">Normally one would choose Basic and then promote users manually via an Admin login (AppBlade needs to configure either an email-based admin login in advance or promote a user on behalf of the customer after login).</span></span>

<span data-ttu-id="680d2-197">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="680d2-197">There is no action item for you in this section.</span></span> <span data-ttu-id="680d2-198">Een nieuwe gebruiker is gemaakt tijdens een poging tot toegang tot AppBlade als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="680d2-198">A new user is created during an attempt to access AppBlade if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="680d2-199">Als u een gebruiker handmatig maken wilt, moet u contact op met de [AppBlade ondersteuningsteam](mailto:support@appblade.com).</span><span class="sxs-lookup"><span data-stu-id="680d2-199">If you need to create a user manually, you need to contact the [AppBlade support team](mailto:support@appblade.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="680d2-200">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="680d2-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="680d2-201">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan AppBlade.</span><span class="sxs-lookup"><span data-stu-id="680d2-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AppBlade.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="680d2-203">**Britta Simon om aan te wijzen AppBlade, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="680d2-203">**To assign Britta Simon to AppBlade, perform the following steps:**</span></span>

1. <span data-ttu-id="680d2-204">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="680d2-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="680d2-206">Selecteer in de lijst met toepassingen **AppBlade**.</span><span class="sxs-lookup"><span data-stu-id="680d2-206">In the applications list, select **AppBlade**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_app.png) 

3. <span data-ttu-id="680d2-208">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="680d2-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="680d2-210">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="680d2-210">Click **Add** button.</span></span> <span data-ttu-id="680d2-211">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="680d2-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="680d2-213">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="680d2-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="680d2-214">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="680d2-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="680d2-215">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="680d2-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="680d2-216">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="680d2-216">Testing single sign-on</span></span>

<span data-ttu-id="680d2-217">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="680d2-217">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="680d2-218">Als u op de tegel AppBlade in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing AppBlade.</span><span class="sxs-lookup"><span data-stu-id="680d2-218">When you click the AppBlade tile in the Access Panel, you should get automatically signed-on to your AppBlade application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="680d2-219">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="680d2-219">Additional resources</span></span>

* [<span data-ttu-id="680d2-220">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="680d2-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="680d2-221">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="680d2-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_203.png

