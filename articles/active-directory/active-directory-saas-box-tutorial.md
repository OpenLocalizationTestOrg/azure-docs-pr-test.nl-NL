---
title: 'Zelfstudie: Azure Active Directory-integratie met vak | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en vak.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5f3517f8-30f2-4be7-9e47-43d702701797
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 2cc2afe8ff3f0063224c94eb0b8135347051b0aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-box"></a><span data-ttu-id="8e5b8-103">Zelfstudie: Azure Active Directory-integratie met het selectievakje</span><span class="sxs-lookup"><span data-stu-id="8e5b8-103">Tutorial: Azure Active Directory integration with Box</span></span>

<span data-ttu-id="8e5b8-104">In deze zelfstudie leert u het selectievakje integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8e5b8-104">In this tutorial, you learn how to integrate Box with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8e5b8-105">Vak integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="8e5b8-105">Integrating Box with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8e5b8-106">U kunt beheren in Azure AD die toegang tot het selectievakje heeft</span><span class="sxs-lookup"><span data-stu-id="8e5b8-106">You can control in Azure AD who has access to Box</span></span>
- <span data-ttu-id="8e5b8-107">U kunt uw gebruikers automatisch ophalen aangemeld bij vak (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="8e5b8-107">You can enable your users to automatically get signed-on to Box (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8e5b8-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="8e5b8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8e5b8-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8e5b8-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e5b8-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8e5b8-110">Prerequisites</span></span>

<span data-ttu-id="8e5b8-111">Voor het configureren van Azure AD-integratie met Box, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="8e5b8-111">To configure Azure AD integration with Box, you need the following items:</span></span>

- <span data-ttu-id="8e5b8-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="8e5b8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8e5b8-113">Een selectievakje eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="8e5b8-113">A Box single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8e5b8-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8e5b8-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="8e5b8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8e5b8-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8e5b8-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8e5b8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8e5b8-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="8e5b8-118">Scenario description</span></span>
<span data-ttu-id="8e5b8-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8e5b8-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="8e5b8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8e5b8-121">Vak uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="8e5b8-121">Adding Box from the gallery</span></span>
2. <span data-ttu-id="8e5b8-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="8e5b8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-box-from-the-gallery"></a><span data-ttu-id="8e5b8-123">Vak uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="8e5b8-123">Adding Box from the gallery</span></span>
<span data-ttu-id="8e5b8-124">Voor het configureren van de integratie van het selectievakje in Azure AD, moet u het selectievakje uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-124">To configure the integration of Box into Azure AD, you need to add Box from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8e5b8-125">**Als u wilt toevoegen het selectievakje uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="8e5b8-125">**To add Box from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8e5b8-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8e5b8-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8e5b8-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="8e5b8-131">Klik op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-131">Click **New application** button on the top of the dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="8e5b8-133">Typ in het zoekvak **vak**.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-133">In the search box, type **Box**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-box-tutorial/tutorial_box_search.png)

5. <span data-ttu-id="8e5b8-135">Selecteer in het deelvenster resultaten **vak**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-135">In the results panel, select **Box**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-box-tutorial/tutorial_box_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8e5b8-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="8e5b8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8e5b8-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met vak op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="8e5b8-138">In this section, you configure and test Azure AD single sign-on with Box based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8e5b8-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in vak is aan een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Box is to a user in Azure AD.</span></span> <span data-ttu-id="8e5b8-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in het vak tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-140">In other words, a link relationship between an Azure AD user and the related user in Box needs to be established.</span></span>

<span data-ttu-id="8e5b8-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in vak.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Box.</span></span>

<span data-ttu-id="8e5b8-142">Als u wilt configureren en Azure AD eenmalige aanmelding met vak testen, moet u voltooien van de volgende elementen:</span><span class="sxs-lookup"><span data-stu-id="8e5b8-142">To configure and test Azure AD single sign-on with Box, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8e5b8-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8e5b8-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8e5b8-145">**[Maken van een gebruiker vak testen](#creating-a-box-test-user)**  - hebben een equivalent van Britta Simon in dat is gekoppeld aan de Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-145">**[Creating a Box test user](#creating-a-box-test-user)** - to have a counterpart of Britta Simon in Box that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8e5b8-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8e5b8-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8e5b8-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="8e5b8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8e5b8-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing vak.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Box application.</span></span>

<span data-ttu-id="8e5b8-150">**Voor het configureren van Azure AD eenmalige aanmelding met Box, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="8e5b8-150">**To configure Azure AD single sign-on with Box, perform the following steps:**</span></span>

1. <span data-ttu-id="8e5b8-151">In de Azure-portal op de **vak** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-151">In the Azure portal, on the **Box** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="8e5b8-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-box-tutorial/tutorial_box_samlbase.png)

3. <span data-ttu-id="8e5b8-155">Op de **in het domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="8e5b8-155">On the **Box Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-box-tutorial/tutorial_box_url.png)

    <span data-ttu-id="8e5b8-157">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<subdomain>.box.com`</span><span class="sxs-lookup"><span data-stu-id="8e5b8-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.box.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8e5b8-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-158">This value is not real.</span></span> <span data-ttu-id="8e5b8-159">Werk de waarde met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-159">Update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="8e5b8-160">Neem contact op met [Box Client ondersteuningsteam](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-160">Contact [Box Client support team](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) to get this value.</span></span> 
 
4. <span data-ttu-id="8e5b8-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-box-tutorial/tutorial_box_certificate.png) 

5. <span data-ttu-id="8e5b8-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-box-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8e5b8-165">Als u eenmalige aanmelding die zijn geconfigureerd voor uw toepassing, neem contact op met [Box Client ondersteuningsteam](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) en geeft u het gedownloade XML-bestand.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-165">To get SSO configured for your application, Contact [Box Client support team](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) and provide them with the downloaded XML file.</span></span>

> [!TIP]
> <span data-ttu-id="8e5b8-166">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="8e5b8-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8e5b8-167">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8e5b8-168">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8e5b8-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8e5b8-169">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="8e5b8-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="8e5b8-170">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="8e5b8-172">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="8e5b8-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8e5b8-173">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-box-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8e5b8-175">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-175">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-box-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8e5b8-177">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-177">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-box-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8e5b8-179">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="8e5b8-179">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-box-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8e5b8-181">a.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-181">a.</span></span> <span data-ttu-id="8e5b8-182">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-182">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8e5b8-183">b.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-183">b.</span></span> <span data-ttu-id="8e5b8-184">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-184">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8e5b8-185">c.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-185">c.</span></span> <span data-ttu-id="8e5b8-186">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-186">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8e5b8-187">d.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-187">d.</span></span> <span data-ttu-id="8e5b8-188">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-188">Click **Create**.</span></span>
 
### <a name="creating-a-box-test-user"></a><span data-ttu-id="8e5b8-189">Maken van een gebruiker vak testen</span><span class="sxs-lookup"><span data-stu-id="8e5b8-189">Creating a Box test user</span></span>

<span data-ttu-id="8e5b8-190">In deze sectie wordt een gebruiker met de naam Britta Simon gemaakt in het vak.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-190">In this section, a user called Britta Simon is created in Box.</span></span> <span data-ttu-id="8e5b8-191">Vak ondersteunt just-in-time-inrichting, die standaard is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-191">Box supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="8e5b8-192">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-192">There is no action item for you in this section.</span></span> <span data-ttu-id="8e5b8-193">Als een gebruiker in het vak nog niet bestaat, wordt een nieuwe gemaakt wanneer u probeert te krijgen tot vak.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-193">If a user doesn't already exist in Box, a new one is created when you attempt to access Box.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8e5b8-194">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e5b8-194">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8e5b8-195">In deze sectie maakt inschakelen u Britta Simon gebruikt Azure eenmalige aanmelding toegang te verlenen aan vak.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Box.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="8e5b8-197">**Als u wilt toewijzen Britta Simon aan vak, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="8e5b8-197">**To assign Britta Simon to Box, perform the following steps:**</span></span>

1. <span data-ttu-id="8e5b8-198">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="8e5b8-200">Selecteer in de lijst met toepassingen **vak**.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-200">In the applications list, select **Box**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-box-tutorial/tutorial_box_app.png) 

3. <span data-ttu-id="8e5b8-202">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-202">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="8e5b8-204">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-204">Click **Add** button.</span></span> <span data-ttu-id="8e5b8-205">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="8e5b8-207">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8e5b8-208">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8e5b8-209">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8e5b8-210">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="8e5b8-210">Testing single sign-on</span></span>

<span data-ttu-id="8e5b8-211">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8e5b8-212">Als u op de tegel vak in het deelvenster toegang, krijgt u de aanmeldingspagina te verkrijgen aangemeld bij uw toepassing vak.</span><span class="sxs-lookup"><span data-stu-id="8e5b8-212">When you click the Box tile in the Access Panel, you should get login page to get signed-on to your Box application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8e5b8-213">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="8e5b8-213">Additional resources</span></span>

* [<span data-ttu-id="8e5b8-214">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8e5b8-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8e5b8-215">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8e5b8-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="8e5b8-216">Gebruikers inrichten configureren</span><span class="sxs-lookup"><span data-stu-id="8e5b8-216">Configure User Provisioning</span></span>](active-directory-saas-box-userprovisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-box-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-box-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-box-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-box-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-box-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-box-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-box-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-box-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-box-tutorial/tutorial_general_203.png

