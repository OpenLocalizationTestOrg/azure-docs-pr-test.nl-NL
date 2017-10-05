---
title: 'Zelfstudie: Azure Active Directory-integratie met MaxxPoint | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en MaxxPoint.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ba026e-96fc-4ae8-b135-0169da810e99
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: 8a7481b71df5ca407dbed5da3d3cc26991504c82
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-maxxpoint"></a><span data-ttu-id="29ae0-103">Zelfstudie: Azure Active Directory-integratie met MaxxPoint</span><span class="sxs-lookup"><span data-stu-id="29ae0-103">Tutorial: Azure Active Directory integration with MaxxPoint</span></span>

<span data-ttu-id="29ae0-104">In deze zelfstudie leert u hoe MaxxPoint integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="29ae0-104">In this tutorial, you learn how to integrate MaxxPoint with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="29ae0-105">MaxxPoint integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="29ae0-105">Integrating MaxxPoint with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="29ae0-106">U kunt beheren in Azure AD die toegang tot MaxxPoint heeft</span><span class="sxs-lookup"><span data-stu-id="29ae0-106">You can control in Azure AD who has access to MaxxPoint</span></span>
- <span data-ttu-id="29ae0-107">U kunt uw gebruikers automatisch ophalen aangemeld bij MaxxPoint (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="29ae0-107">You can enable your users to automatically get signed-on to MaxxPoint (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="29ae0-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="29ae0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="29ae0-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="29ae0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29ae0-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="29ae0-110">Prerequisites</span></span>

<span data-ttu-id="29ae0-111">Voor het configureren van Azure AD-integratie met MaxxPoint, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="29ae0-111">To configure Azure AD integration with MaxxPoint, you need the following items:</span></span>

- <span data-ttu-id="29ae0-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="29ae0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="29ae0-113">Een MaxxPoint eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="29ae0-113">A MaxxPoint single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="29ae0-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="29ae0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="29ae0-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="29ae0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="29ae0-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="29ae0-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="29ae0-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="29ae0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="29ae0-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="29ae0-118">Scenario description</span></span>
<span data-ttu-id="29ae0-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="29ae0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="29ae0-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="29ae0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="29ae0-121">MaxxPoint uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="29ae0-121">Adding MaxxPoint from the gallery</span></span>
2. <span data-ttu-id="29ae0-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="29ae0-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-maxxpoint-from-the-gallery"></a><span data-ttu-id="29ae0-123">MaxxPoint uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="29ae0-123">Adding MaxxPoint from the gallery</span></span>
<span data-ttu-id="29ae0-124">Voor het configureren van de integratie van MaxxPoint in Azure AD, moet u MaxxPoint uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="29ae0-124">To configure the integration of MaxxPoint into Azure AD, you need to add MaxxPoint from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="29ae0-125">**Als u wilt toevoegen MaxxPoint uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="29ae0-125">**To add MaxxPoint from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="29ae0-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="29ae0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="29ae0-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="29ae0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="29ae0-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="29ae0-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="29ae0-131">Klik op **nieuwe toepassing** knop boven aan het dialoogvenster nieuwe toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="29ae0-131">Click **New application** button on the top of dialog to add new application.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="29ae0-133">Typ in het zoekvak **MaxxPoint**.</span><span class="sxs-lookup"><span data-stu-id="29ae0-133">In the search box, type **MaxxPoint**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_001.png)

5. <span data-ttu-id="29ae0-135">Selecteer in het deelvenster resultaten **MaxxPoint**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="29ae0-135">In the results panel, select **MaxxPoint**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="29ae0-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="29ae0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="29ae0-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met MaxxPoint op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="29ae0-138">In this section, you configure and test Azure AD single sign-on with MaxxPoint based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="29ae0-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in MaxxPoint is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29ae0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in MaxxPoint is to a user in Azure AD.</span></span> <span data-ttu-id="29ae0-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in MaxxPoint tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="29ae0-140">In other words, a link relationship between an Azure AD user and the related user in MaxxPoint needs to be established.</span></span>

<span data-ttu-id="29ae0-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="29ae0-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in MaxxPoint.</span></span>

<span data-ttu-id="29ae0-142">Om te configureren en testen van Azure AD eenmalige aanmelding met MaxxPoint, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="29ae0-142">To configure and test Azure AD single sign-on with MaxxPoint, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="29ae0-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="29ae0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="29ae0-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="29ae0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="29ae0-145">**[Maken van een testgebruiker MaxxPoint](#creating-a-maxxpoint-test-user)**  - MaxxPoint die is gekoppeld aan de Azure AD-representatie van haar van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="29ae0-145">**[Creating a MaxxPoint test user](#creating-a-maxxpoint-test-user)** - to have a counterpart of Britta Simon in MaxxPoint that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="29ae0-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="29ae0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="29ae0-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="29ae0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="29ae0-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="29ae0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="29ae0-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing MaxxPoint configureren.</span><span class="sxs-lookup"><span data-stu-id="29ae0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your MaxxPoint application.</span></span>

<span data-ttu-id="29ae0-150">**Voor het configureren van Azure AD eenmalige aanmelding met MaxxPoint, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="29ae0-150">**To configure Azure AD single sign-on with MaxxPoint, perform the following steps:**</span></span>

1. <span data-ttu-id="29ae0-151">In de Azure-portal op de **MaxxPoint** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="29ae0-151">In the Azure portal, on the **MaxxPoint** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="29ae0-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="29ae0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_300.png)

3. <span data-ttu-id="29ae0-155">Op de **MaxxPoint domein en de URL's** sectie als u wilt configureren van de toepassing in **IDP geïnitieerd modus**, hoeft u niet alle stappen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="29ae0-155">On the **MaxxPoint Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, no need to perform any steps.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_02.png)
    
4. <span data-ttu-id="29ae0-157">Op de **MaxxPoint domein en de URL's** sectie als u wilt configureren van de toepassing in **SP geïnitieerd modus**, voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="29ae0-157">On the **MaxxPoint Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_03.png)

    <span data-ttu-id="29ae0-159">a.</span><span class="sxs-lookup"><span data-stu-id="29ae0-159">a.</span></span> <span data-ttu-id="29ae0-160">Klik op **weergeven geavanceerde instellingen voor URL** optie</span><span class="sxs-lookup"><span data-stu-id="29ae0-160">Click **Show advanced URL settings** option</span></span>

    <span data-ttu-id="29ae0-161">b.</span><span class="sxs-lookup"><span data-stu-id="29ae0-161">b.</span></span> <span data-ttu-id="29ae0-162">In de **aanmelding op URL** textbox, typ een URL met het volgende patroon volgen:`https://maxxpoint.westipc.com/default/sso/login/entity/<customer-id>-azure`</span><span class="sxs-lookup"><span data-stu-id="29ae0-162">In the **Sign On URL** textbox, type a URL using the following pattern: `https://maxxpoint.westipc.com/default/sso/login/entity/<customer-id>-azure`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="29ae0-163">Houd er rekening mee dat dit geen de feitelijke waarde is.</span><span class="sxs-lookup"><span data-stu-id="29ae0-163">Please note that this is not the real value.</span></span> <span data-ttu-id="29ae0-164">U moet deze waarde met de werkelijke aanmelding op de URL bijwerken.</span><span class="sxs-lookup"><span data-stu-id="29ae0-164">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="29ae0-165">Aanroepen van MaxxPoint team voor **888-728-0950** deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="29ae0-165">Call MaxxPoint team on **888-728-0950** to get this value.</span></span>

5. <span data-ttu-id="29ae0-166">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="29ae0-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_06.png) 

6. <span data-ttu-id="29ae0-168">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="29ae0-168">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="29ae0-170">Als u eenmalige aanmelding die zijn geconfigureerd voor uw toepassing, ondersteuningsteam MaxxPoint niet aanroepen voor **888-728-0950** en ze helpt u verder gaat over het om ze te bieden de gedownloade **Metadata XML** bestand.</span><span class="sxs-lookup"><span data-stu-id="29ae0-170">To get SSO configured for your application, call MaxxPoint support team on **888-728-0950** and they'll assist you further on how to provide them the downloaded **Metadata XML** file.</span></span> 

> [!TIP]
> <span data-ttu-id="29ae0-171">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="29ae0-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="29ae0-172">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="29ae0-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="29ae0-173">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="29ae0-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="29ae0-174">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="29ae0-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="29ae0-175">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="29ae0-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="29ae0-177">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="29ae0-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="29ae0-178">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="29ae0-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="29ae0-180">Ga naar **gebruikers en groepen** en klik op **alle gebruikers** om de lijst met gebruikers weer te geven.</span><span class="sxs-lookup"><span data-stu-id="29ae0-180">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="29ae0-182">Klik aan de bovenkant van het dialoogvenster **toevoegen** openen de **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="29ae0-182">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="29ae0-184">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="29ae0-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="29ae0-186">a.</span><span class="sxs-lookup"><span data-stu-id="29ae0-186">a.</span></span> <span data-ttu-id="29ae0-187">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="29ae0-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="29ae0-188">b.</span><span class="sxs-lookup"><span data-stu-id="29ae0-188">b.</span></span> <span data-ttu-id="29ae0-189">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="29ae0-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="29ae0-190">c.</span><span class="sxs-lookup"><span data-stu-id="29ae0-190">c.</span></span> <span data-ttu-id="29ae0-191">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="29ae0-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="29ae0-192">d.</span><span class="sxs-lookup"><span data-stu-id="29ae0-192">d.</span></span> <span data-ttu-id="29ae0-193">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="29ae0-193">Click **Create**.</span></span> 

### <a name="creating-a-maxxpoint-test-user"></a><span data-ttu-id="29ae0-194">Een testgebruiker MaxxPoint maken</span><span class="sxs-lookup"><span data-stu-id="29ae0-194">Creating a MaxxPoint test user</span></span>

<span data-ttu-id="29ae0-195">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in MaxxPoint maken.</span><span class="sxs-lookup"><span data-stu-id="29ae0-195">In this section, you create a user called Britta Simon in MaxxPoint.</span></span> <span data-ttu-id="29ae0-196">Neem contact op met het ondersteuningsteam MaxxPoint op **888-728-0950** de gebruikers in de toepassing MaxxPoint toevoegen.</span><span class="sxs-lookup"><span data-stu-id="29ae0-196">Please call MaxxPoint support team on **888-728-0950** to add the users in the MaxxPoint application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="29ae0-197">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="29ae0-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="29ae0-198">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door haar toegang verlenen aan MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="29ae0-198">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to MaxxPoint.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="29ae0-200">**Britta Simon om aan te wijzen MaxxPoint, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="29ae0-200">**To assign Britta Simon to MaxxPoint, perform the following steps:**</span></span>

1. <span data-ttu-id="29ae0-201">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="29ae0-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="29ae0-203">Selecteer in de lijst met toepassingen **MaxxPoint**.</span><span class="sxs-lookup"><span data-stu-id="29ae0-203">In the applications list, select **MaxxPoint**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_50.png) 

3. <span data-ttu-id="29ae0-205">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="29ae0-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="29ae0-207">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="29ae0-207">Click **Add** button.</span></span> <span data-ttu-id="29ae0-208">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="29ae0-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="29ae0-210">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="29ae0-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="29ae0-211">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="29ae0-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="29ae0-212">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="29ae0-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="29ae0-213">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="29ae0-213">Testing single sign-on</span></span>

<span data-ttu-id="29ae0-214">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="29ae0-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="29ae0-215">Als u op de tegel MaxxPoint in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="29ae0-215">When you click the MaxxPoint tile in the Access Panel, you should get automatically signed-on to your MaxxPoint application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="29ae0-216">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="29ae0-216">Additional resources</span></span>

* [<span data-ttu-id="29ae0-217">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="29ae0-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="29ae0-218">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="29ae0-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_203.png