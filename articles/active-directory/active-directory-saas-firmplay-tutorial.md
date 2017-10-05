---
title: 'Zelfstudie: Azure Active Directory-integratie met FirmPlay - werknemer Advocacy voor werving | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en FirmPlay - werknemer Advocacy voor werving.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a6799629-7546-43f8-a966-956db32864b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: 3cddd5b9508159089bf344dbb3882d462799747c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-firmplay---employee-advocacy-for-recruiting"></a><span data-ttu-id="99cb1-103">Zelfstudie: Azure Active Directory-integratie met FirmPlay - werknemer Advocacy voor werving</span><span class="sxs-lookup"><span data-stu-id="99cb1-103">Tutorial: Azure Active Directory integration with FirmPlay - Employee Advocacy for Recruiting</span></span>

<span data-ttu-id="99cb1-104">In deze zelfstudie leert u hoe integreren FirmPlay - werknemer Advocacy voor werving met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="99cb1-104">In this tutorial, you learn how to integrate FirmPlay - Employee Advocacy for Recruiting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="99cb1-105">Integratie van FirmPlay - werknemer Advocacy voor werving met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="99cb1-105">Integrating FirmPlay - Employee Advocacy for Recruiting with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="99cb1-106">U kunt beheren in Azure AD die toegang tot FirmPlay - werknemer Advocacy voor werving heeft</span><span class="sxs-lookup"><span data-stu-id="99cb1-106">You can control in Azure AD who has access to FirmPlay - Employee Advocacy for Recruiting</span></span>
- <span data-ttu-id="99cb1-107">U kunt uw gebruikers automatisch ophalen aangemeld bij FirmPlay - werknemer Advocacy voor werving (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="99cb1-107">You can enable your users to automatically get signed-on to FirmPlay - Employee Advocacy for Recruiting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="99cb1-108">U kunt uw accounts op één centrale locatie - en de Azure Management portal beheren</span><span class="sxs-lookup"><span data-stu-id="99cb1-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="99cb1-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="99cb1-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99cb1-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="99cb1-110">Prerequisites</span></span>

<span data-ttu-id="99cb1-111">Voor het configureren van Azure AD-integratie met FirmPlay - werknemer Advocacy voor werving, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="99cb1-111">To configure Azure AD integration with FirmPlay - Employee Advocacy for Recruiting, you need the following items:</span></span>

- <span data-ttu-id="99cb1-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="99cb1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="99cb1-113">Een FirmPlay - werknemer Advocacy voor het werven van eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="99cb1-113">A FirmPlay - Employee Advocacy for Recruiting single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="99cb1-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="99cb1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="99cb1-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="99cb1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="99cb1-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="99cb1-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="99cb1-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="99cb1-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="99cb1-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="99cb1-118">Scenario description</span></span>
<span data-ttu-id="99cb1-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="99cb1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="99cb1-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="99cb1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="99cb1-121">FirmPlay - werknemer Advocacy voor werving uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="99cb1-121">Adding FirmPlay - Employee Advocacy for Recruiting from the gallery</span></span>
2. <span data-ttu-id="99cb1-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="99cb1-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-firmplay---employee-advocacy-for-recruiting-from-the-gallery"></a><span data-ttu-id="99cb1-123">FirmPlay - werknemer Advocacy voor werving uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="99cb1-123">Adding FirmPlay - Employee Advocacy for Recruiting from the gallery</span></span>
<span data-ttu-id="99cb1-124">Voor het configureren van de integratie van FirmPlay - werknemer Advocacy voor werving in Azure AD, moet u FirmPlay - werknemer Advocacy voor werving uit de galerie aan de lijst met beheerde SaaS-apps toevoegen.</span><span class="sxs-lookup"><span data-stu-id="99cb1-124">To configure the integration of FirmPlay - Employee Advocacy for Recruiting into Azure AD, you need to add FirmPlay - Employee Advocacy for Recruiting from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="99cb1-125">**Als u wilt toevoegen, FirmPlay - werknemer Advocacy voor werving uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="99cb1-125">**To add FirmPlay - Employee Advocacy for Recruiting from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="99cb1-126">In de  **[Azure Management Portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="99cb1-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="99cb1-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="99cb1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="99cb1-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="99cb1-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="99cb1-131">Klik op **toevoegen** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="99cb1-131">Click **Add** button on the top of the dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="99cb1-133">Typ in het zoekvak **FirmPlay - werknemer Advocacy voor werving**.</span><span class="sxs-lookup"><span data-stu-id="99cb1-133">In the search box, type **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_001.png)

5. <span data-ttu-id="99cb1-135">Selecteer in het deelvenster resultaten **FirmPlay - werknemer Advocacy voor werving**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="99cb1-135">In the results panel, select **FirmPlay - Employee Advocacy for Recruiting**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="99cb1-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="99cb1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="99cb1-138">In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met FirmPlay - werknemer Advocacy voor werving op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="99cb1-138">In this section, you configure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="99cb1-139">Azure AD moet weten wat de equivalente gebruiker in FirmPlay - werknemer Advocacy voor werving is aan een gebruiker in Azure AD voor eenmalige aanmelding werkt.</span><span class="sxs-lookup"><span data-stu-id="99cb1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FirmPlay - Employee Advocacy for Recruiting is to a user in Azure AD.</span></span> <span data-ttu-id="99cb1-140">Met andere woorden, een relatie koppeling tussen een Azure AD-gebruiker en de betreffende gebruiker in FirmPlay - werknemer Advocacy voor het werven van moet tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="99cb1-140">In other words, a link relationship between an Azure AD user and the related user in FirmPlay - Employee Advocacy for Recruiting needs to be established.</span></span>

<span data-ttu-id="99cb1-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in FirmPlay - werknemer Advocacy voor werving.</span><span class="sxs-lookup"><span data-stu-id="99cb1-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FirmPlay - Employee Advocacy for Recruiting.</span></span>

<span data-ttu-id="99cb1-142">Als u wilt configureren en testen Azure AD eenmalige aanmelding met FirmPlay - werknemer Advocacy voor werving, moet u de volgende elementen voltooid:</span><span class="sxs-lookup"><span data-stu-id="99cb1-142">To configure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="99cb1-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="99cb1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="99cb1-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="99cb1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="99cb1-145">**[Maken van een FirmPlay - werknemer Advocacy voor de testgebruiker werving](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)**  - met een exemplaar van Britta Simon FirmPlay: werknemer Advocacy voor het werven van is gekoppeld aan de Azure AD-representatie van haar.</span><span class="sxs-lookup"><span data-stu-id="99cb1-145">**[Creating a FirmPlay - Employee Advocacy for Recruiting test user](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)** - to have a counterpart of Britta Simon in FirmPlay: Employee Advocacy for Recruiting that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="99cb1-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="99cb1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="99cb1-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="99cb1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="99cb1-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="99cb1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="99cb1-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure-beheerportal en eenmalige aanmelding in uw FirmPlay - werknemer Advocacy voor werving toepassing configureren.</span><span class="sxs-lookup"><span data-stu-id="99cb1-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your FirmPlay - Employee Advocacy for Recruiting application.</span></span>

<span data-ttu-id="99cb1-150">**Voor het configureren van Azure AD eenmalige aanmelding met FirmPlay - werknemer Advocacy voor werving, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="99cb1-150">**To configure Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, perform the following steps:**</span></span>

1. <span data-ttu-id="99cb1-151">In de Azure-beheerportal op de **FirmPlay - werknemer Advocacy voor werving** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="99cb1-151">In the Azure Management portal, on the **FirmPlay - Employee Advocacy for Recruiting** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="99cb1-153">Op de **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** eenmalige aanmelding inschakelen op.</span><span class="sxs-lookup"><span data-stu-id="99cb1-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_01.png)

3. <span data-ttu-id="99cb1-155">Op de **FirmPlay - werknemer Advocacy voor het werven van domein en de URL's** sectie in het **aanmelding op URL** textbox, typ een URL met het volgende patroon volgen:`https://<your-subdomain>.firmplay.com/`</span><span class="sxs-lookup"><span data-stu-id="99cb1-155">On the **FirmPlay - Employee Advocacy for Recruiting Domain and URLs** section, in the **Sign On URL** textbox, type a URL using the following pattern: `https://<your-subdomain>.firmplay.com/`</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_02.png)

    > [!NOTE] 
    > <span data-ttu-id="99cb1-157">Houd er rekening mee dat dit geen de feitelijke waarde is.</span><span class="sxs-lookup"><span data-stu-id="99cb1-157">Please note that this is not the real value.</span></span> <span data-ttu-id="99cb1-158">U moet deze waarde met de werkelijke aanmelding op de URL bijwerken.</span><span class="sxs-lookup"><span data-stu-id="99cb1-158">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="99cb1-159">Neem contact op met [FirmPlay - werknemer Advocacy voor werving ondersteuningsteam](mailto:engineering@firmplay.com) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="99cb1-159">Contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) to get this value.</span></span> 

4. <span data-ttu-id="99cb1-160">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **nieuw certificaat maken**.</span><span class="sxs-lookup"><span data-stu-id="99cb1-160">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_03.png)   

5. <span data-ttu-id="99cb1-162">Op de **nieuw certificaat maken** dialoogvenster, klikt u op het pictogram van de kalender en selecteer een **vervaldatum**.</span><span class="sxs-lookup"><span data-stu-id="99cb1-162">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="99cb1-163">Klik vervolgens op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="99cb1-163">Then click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-firmplay-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="99cb1-165">Op de **SAML-certificaat voor ondertekening van** sectie **nieuwe certificaat activeren** en klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="99cb1-165">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_04.png)

7. <span data-ttu-id="99cb1-167">In het pop-upvenster **rollovercertificaat** venster, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="99cb1-167">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-firmplay-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="99cb1-169">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="99cb1-169">On the **SAML Signing Certificate** section, click **Certificate (base64)** and then save the certificate file on your computer.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_05.png) 

9. <span data-ttu-id="99cb1-171">Op de **FirmPlay - werknemer Advocacy voor configuratie werven** sectie, klikt u op **configureren FirmPlay - werknemer Advocacy voor werving** openen **eenmalige aanmelding configureren** het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="99cb1-171">On the **FirmPlay - Employee Advocacy for Recruiting Configuration** section, click **Configure FirmPlay - Employee Advocacy for Recruiting** to open **Configure sign-on** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_06.png) 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_07.png)

10. <span data-ttu-id="99cb1-174">Als u eenmalige aanmelding die zijn geconfigureerd voor uw toepassing, neem contact op met [FirmPlay - werknemer Advocacy voor werving ondersteuningsteam](mailto:engineering@firmplay.com) en geeft u het volgende:</span><span class="sxs-lookup"><span data-stu-id="99cb1-174">To get SSO configured for your application, contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) and provide them with the following:</span></span> 

    <span data-ttu-id="99cb1-175">• De gedownloade **certificaatbestand**</span><span class="sxs-lookup"><span data-stu-id="99cb1-175">•  The downloaded **Certificate file**</span></span>

    <span data-ttu-id="99cb1-176">• De **URL voor SAML-Service voor eenmalige aanmelding**</span><span class="sxs-lookup"><span data-stu-id="99cb1-176">•  The **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="99cb1-177">• De **SAML entiteit-ID**</span><span class="sxs-lookup"><span data-stu-id="99cb1-177">•  The **SAML Entity ID**</span></span>

    <span data-ttu-id="99cb1-178">• De **afmelden URL**</span><span class="sxs-lookup"><span data-stu-id="99cb1-178">•  The **Sign-Out URL**</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="99cb1-179">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="99cb1-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="99cb1-180">Het doel van deze sectie is het een testgebruiker maken in Azure Management portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="99cb1-180">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="99cb1-182">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="99cb1-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="99cb1-183">In de **Azure Management portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="99cb1-183">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-firmplay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="99cb1-185">Ga naar **gebruikers en groepen** en klik op **alle gebruikers** om de lijst met gebruikers weer te geven.</span><span class="sxs-lookup"><span data-stu-id="99cb1-185">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-firmplay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="99cb1-187">Klik aan de bovenkant van het dialoogvenster **toevoegen** openen de **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="99cb1-187">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-firmplay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="99cb1-189">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="99cb1-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-firmplay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="99cb1-191">a.</span><span class="sxs-lookup"><span data-stu-id="99cb1-191">a.</span></span> <span data-ttu-id="99cb1-192">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="99cb1-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="99cb1-193">b.</span><span class="sxs-lookup"><span data-stu-id="99cb1-193">b.</span></span> <span data-ttu-id="99cb1-194">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="99cb1-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="99cb1-195">c.</span><span class="sxs-lookup"><span data-stu-id="99cb1-195">c.</span></span> <span data-ttu-id="99cb1-196">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="99cb1-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="99cb1-197">d.</span><span class="sxs-lookup"><span data-stu-id="99cb1-197">d.</span></span> <span data-ttu-id="99cb1-198">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="99cb1-198">Click **Create**.</span></span> 



### <a name="creating-a-firmplay---employee-advocacy-for-recruiting-test-user"></a><span data-ttu-id="99cb1-199">Maken van een FirmPlay - werknemer Advocacy voor werving testgebruiker</span><span class="sxs-lookup"><span data-stu-id="99cb1-199">Creating a FirmPlay - Employee Advocacy for Recruiting test user</span></span>

<span data-ttu-id="99cb1-200">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in FirmPlay - werknemer Advocacy voor werving maken.</span><span class="sxs-lookup"><span data-stu-id="99cb1-200">In this section, you create a user called Britta Simon in FirmPlay - Employee Advocacy for Recruiting.</span></span> <span data-ttu-id="99cb1-201">Neem contact op met [FirmPlay - werknemer Advocacy voor werving ondersteuningsteam](mailto:engineering@firmplay.com) toevoegen van de gebruikers in de FirmPlay - werknemer Advocacy voor werving platform.</span><span class="sxs-lookup"><span data-stu-id="99cb1-201">Please work with [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) to add the users in the FirmPlay - Employee Advocacy for Recruiting platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="99cb1-202">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="99cb1-202">Assigning the Azure AD test user</span></span>

<span data-ttu-id="99cb1-203">In deze sectie maakt inschakelen u Britta Simon Azure eenmalige aanmelding gebruiken door haar toegang verlenen aan FirmPlay - werknemer Advocacy voor werving.</span><span class="sxs-lookup"><span data-stu-id="99cb1-203">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to FirmPlay - Employee Advocacy for Recruiting.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="99cb1-205">**Britta Simon om aan te wijzen FirmPlay - werknemer Advocacy voor werving, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="99cb1-205">**To assign Britta Simon to FirmPlay - Employee Advocacy for Recruiting, perform the following steps:**</span></span>

1. <span data-ttu-id="99cb1-206">In de Azure-beheerportal, opent u de weergave toepassingen en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="99cb1-206">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="99cb1-208">Selecteer in de lijst met toepassingen **FirmPlay - werknemer Advocacy voor werving**.</span><span class="sxs-lookup"><span data-stu-id="99cb1-208">In the applications list, select **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_50.png) 

3. <span data-ttu-id="99cb1-210">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="99cb1-210">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="99cb1-212">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="99cb1-212">Click **Add** button.</span></span> <span data-ttu-id="99cb1-213">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="99cb1-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="99cb1-215">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="99cb1-215">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="99cb1-216">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="99cb1-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="99cb1-217">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="99cb1-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="99cb1-218">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="99cb1-218">Testing single sign-on</span></span>

<span data-ttu-id="99cb1-219">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="99cb1-219">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="99cb1-220">Wanneer u klikt op de FirmPlay - werknemer Advocacy werving tegel in het deelvenster toegang u moet ophalen automatisch aangemeld bij uw FirmPlay - werknemer Advocacy voor werving toepassing.</span><span class="sxs-lookup"><span data-stu-id="99cb1-220">When you click the FirmPlay - Employee Advocacy for Recruiting tile in the Access Panel, you should get automatically signed-on to your FirmPlay - Employee Advocacy for Recruiting application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="99cb1-221">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="99cb1-221">Additional resources</span></span>

* [<span data-ttu-id="99cb1-222">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="99cb1-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="99cb1-223">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="99cb1-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_203.png