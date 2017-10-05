---
title: 'Zelfstudie: Azure Active Directory-integratie met PlanMyLeave | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en PlanMyLeave.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b0d31cbe-7ae2-488b-9cf3-4927391fa744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: jeedes
ms.openlocfilehash: ba418a641b339a0d94a3c7b2596d37fbd88a30c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-planmyleave"></a><span data-ttu-id="6d701-103">Zelfstudie: Azure Active Directory-integratie met PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="6d701-103">Tutorial: Azure Active Directory integration with PlanMyLeave</span></span>

<span data-ttu-id="6d701-104">In deze zelfstudie leert u hoe PlanMyLeave integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6d701-104">In this tutorial, you learn how to integrate PlanMyLeave with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6d701-105">PlanMyLeave integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="6d701-105">Integrating PlanMyLeave with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6d701-106">U kunt beheren in Azure AD die toegang tot PlanMyLeave heeft</span><span class="sxs-lookup"><span data-stu-id="6d701-106">You can control in Azure AD who has access to PlanMyLeave</span></span>
- <span data-ttu-id="6d701-107">U kunt uw gebruikers automatisch ophalen aangemeld bij PlanMyLeave (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="6d701-107">You can enable your users to automatically get signed-on to PlanMyLeave (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6d701-108">U kunt uw accounts op één centrale locatie - en de Azure Management portal beheren</span><span class="sxs-lookup"><span data-stu-id="6d701-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="6d701-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6d701-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d701-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6d701-110">Prerequisites</span></span>

<span data-ttu-id="6d701-111">Voor het configureren van Azure AD-integratie met PlanMyLeave, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="6d701-111">To configure Azure AD integration with PlanMyLeave, you need the following items:</span></span>

- <span data-ttu-id="6d701-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="6d701-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6d701-113">Een PlanMyLeave eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="6d701-113">A PlanMyLeave single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="6d701-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="6d701-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="6d701-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="6d701-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6d701-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="6d701-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="6d701-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6d701-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="6d701-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="6d701-118">Scenario description</span></span>
<span data-ttu-id="6d701-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="6d701-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6d701-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="6d701-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6d701-121">PlanMyLeave uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="6d701-121">Adding PlanMyLeave from the gallery</span></span>
2. <span data-ttu-id="6d701-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6d701-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-planmyleave-from-the-gallery"></a><span data-ttu-id="6d701-123">PlanMyLeave uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="6d701-123">Adding PlanMyLeave from the gallery</span></span>
<span data-ttu-id="6d701-124">Voor het configureren van de integratie van PlanMyLeave in Azure AD, moet u PlanMyLeave uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="6d701-124">To configure the integration of PlanMyLeave into Azure AD, you need to add PlanMyLeave from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6d701-125">**Als u wilt toevoegen PlanMyLeave uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6d701-125">**To add PlanMyLeave from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6d701-126">In de  **[Azure Management Portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6d701-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6d701-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6d701-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6d701-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6d701-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="6d701-131">Klik op **toevoegen** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6d701-131">Click **Add** button on the top of the dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="6d701-133">Typ in het zoekvak **PlanMyLeave**.</span><span class="sxs-lookup"><span data-stu-id="6d701-133">In the search box, type **PlanMyLeave**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_001.png)

5. <span data-ttu-id="6d701-135">Selecteer in het deelvenster resultaten **PlanMyLeave**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="6d701-135">In the results panel, select **PlanMyLeave**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6d701-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6d701-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6d701-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met PlanMyLeave op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="6d701-138">In this section, you configure and test Azure AD single sign-on with PlanMyLeave based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6d701-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in PlanMyLeave is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d701-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PlanMyLeave is to a user in Azure AD.</span></span> <span data-ttu-id="6d701-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in PlanMyLeave tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="6d701-140">In other words, a link relationship between an Azure AD user and the related user in PlanMyLeave needs to be established.</span></span>

<span data-ttu-id="6d701-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="6d701-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in PlanMyLeave.</span></span>

<span data-ttu-id="6d701-142">Om te configureren en testen van Azure AD eenmalige aanmelding met PlanMyLeave, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="6d701-142">To configure and test Azure AD single sign-on with PlanMyLeave, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6d701-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6d701-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6d701-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6d701-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6d701-145">**[Maken van een testgebruiker PlanMyLeave](#creating-a-planmyleave-test-user)**  - PlanMyLeave die is gekoppeld aan de Azure AD-representatie van haar van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="6d701-145">**[Creating a PlanMyLeave test user](#creating-a-planmyleave-test-user)** - to have a counterpart of Britta Simon in PlanMyLeave that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="6d701-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="6d701-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6d701-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="6d701-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6d701-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="6d701-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6d701-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure-beheerportal en eenmalige aanmelding in uw toepassing PlanMyLeave configureren.</span><span class="sxs-lookup"><span data-stu-id="6d701-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your PlanMyLeave application.</span></span>

<span data-ttu-id="6d701-150">**Voor het configureren van Azure AD eenmalige aanmelding met PlanMyLeave, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6d701-150">**To configure Azure AD single sign-on with PlanMyLeave, perform the following steps:**</span></span>

1. <span data-ttu-id="6d701-151">In de Azure-beheerportal op de **PlanMyLeave** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="6d701-151">In the Azure Management portal, on the **PlanMyLeave** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="6d701-153">Op de **eenmalige aanmelding** dialoogvenster pagina als **modus** Selecteer **op basis van SAML aanmelding** eenmalige aanmelding inschakelen op.</span><span class="sxs-lookup"><span data-stu-id="6d701-153">On the **Single sign-on** dialog page, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_01.png)

3. <span data-ttu-id="6d701-155">Op de **PlanMyLeave domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6d701-155">On the **PlanMyLeave Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_02.png)

    <span data-ttu-id="6d701-157">a.</span><span class="sxs-lookup"><span data-stu-id="6d701-157">a.</span></span> <span data-ttu-id="6d701-158">In de **aanmelding op URL** textbox, typ een URL met het volgende patroon volgen:`https://<company-name>.planmyleave.com/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="6d701-158">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company-name>.planmyleave.com/Login.aspx`</span></span>
    
    <span data-ttu-id="6d701-159">b.</span><span class="sxs-lookup"><span data-stu-id="6d701-159">b.</span></span> <span data-ttu-id="6d701-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<company-name>.planmyleave.com`</span><span class="sxs-lookup"><span data-stu-id="6d701-160">In the **Identifer** textbox, type a URL using the following pattern: `https://<company-name>.planmyleave.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6d701-161">Houd er rekening mee dat deze niet de werkelijke waarden zijn.</span><span class="sxs-lookup"><span data-stu-id="6d701-161">Please note that these are not the real values.</span></span> <span data-ttu-id="6d701-162">U hebt deze waarden bijwerken met het werkelijke aanmelding op de URL en de id.</span><span class="sxs-lookup"><span data-stu-id="6d701-162">You have to update these values with the actual Sign On URL and Identifier.</span></span> <span data-ttu-id="6d701-163">Neem contact op met [PlanMyLeave ondersteuningsteam](mailto:support@planmyleave.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="6d701-163">Contact [PlanMyLeave support team](mailto:support@planmyleave.com) to get these values.</span></span>

4. <span data-ttu-id="6d701-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **nieuw certificaat maken**.</span><span class="sxs-lookup"><span data-stu-id="6d701-164">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_03.png)     

5. <span data-ttu-id="6d701-166">Op de **nieuw certificaat maken** dialoogvenster, klikt u op het pictogram van de kalender en selecteer een **vervaldatum**.</span><span class="sxs-lookup"><span data-stu-id="6d701-166">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="6d701-167">Klik vervolgens op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="6d701-167">Then click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="6d701-169">Op de **SAML-certificaat voor ondertekening van** sectie **nieuwe certificaat activeren** en klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="6d701-169">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_04.png)

7. <span data-ttu-id="6d701-171">In het pop-upvenster **rollovercertificaat** venster, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="6d701-171">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="6d701-173">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="6d701-173">On the **SAML Signing Certificate** section, click **Certificate (base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_05.png) 

9. <span data-ttu-id="6d701-175">Op de **PlanMyLeave configuratie** sectie, klikt u op **configureren PlanMyLeave** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="6d701-175">On the **PlanMyLeave Configuration** section, click **Configure PlanMyLeave** to open **Configure sign-on** window.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_06.png) 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_07.png)

10. <span data-ttu-id="6d701-178">Meld u aan bij uw tenant PlanMyLeave als een beheerder in een ander browservenster.</span><span class="sxs-lookup"><span data-stu-id="6d701-178">In a different web browser window, log into your PlanMyLeave tenant as an administrator.</span></span>

11. <span data-ttu-id="6d701-179">Ga naar **Setup van System**.</span><span class="sxs-lookup"><span data-stu-id="6d701-179">Go to **System Setup**.</span></span> <span data-ttu-id="6d701-180">Klik op de **beveiligingsbeheer** sectie Klik **bedrijf SAML-instellingen** .</span><span class="sxs-lookup"><span data-stu-id="6d701-180">Then on the **Security Management** section click **Company SAML settings** .</span></span>

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_002.png) 

12. <span data-ttu-id="6d701-182">Op de **SAML instellingen** sectie, klikt u op het pictogram van de editor.</span><span class="sxs-lookup"><span data-stu-id="6d701-182">On the **SAML Settings** section, click editor icon.</span></span>

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_003.png)

13. <span data-ttu-id="6d701-184">Op de **SAML-Update-instellingen** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6d701-184">On the **Update SAML Settings** section, perform the following steps:</span></span>

    ![App-zijde eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_004.png)

    <span data-ttu-id="6d701-186">a.</span><span class="sxs-lookup"><span data-stu-id="6d701-186">a.</span></span>  <span data-ttu-id="6d701-187">In de **aanmeldings-URL** textbox, plaatst u de waarde van **SAML Single Sign-On Service-URL** van het venster voor configuratie van Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="6d701-187">In the **Login URL** textbox, put the value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="6d701-188">b.</span><span class="sxs-lookup"><span data-stu-id="6d701-188">b.</span></span>  <span data-ttu-id="6d701-189">Open het gedownloade certificaatbestand in Kladblok, alleen de inhoud kopiëren tussen het---certificaat begint certificaat--- en---einde---ervan naar het Klembord en plakt u deze naar de **certificaat** textbox.</span><span class="sxs-lookup"><span data-stu-id="6d701-189">Open your downloaded certificate file in notepad, copy only the content between the ---Begin Certificate--- and ---End certificate---- of it into your clipboard, and then paste it to the **Certificate** textbox.</span></span>

    <span data-ttu-id="6d701-190">c.</span><span class="sxs-lookup"><span data-stu-id="6d701-190">c.</span></span> <span data-ttu-id="6d701-191">Stel '**Is ingeschakeld**'tot'**Ja**'.</span><span class="sxs-lookup"><span data-stu-id="6d701-191">Set "**Is Enable**" to "**Yes**".</span></span>

    <span data-ttu-id="6d701-192">d.</span><span class="sxs-lookup"><span data-stu-id="6d701-192">d.</span></span> <span data-ttu-id="6d701-193">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="6d701-193">Click **Save**.</span></span>



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6d701-194">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="6d701-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="6d701-195">Het doel van deze sectie is het een testgebruiker maken in Azure Management portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="6d701-195">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="6d701-197">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6d701-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6d701-198">In de **Azure Management portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="6d701-198">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6d701-200">Ga naar **gebruikers en groepen** en klik op **alle gebruikers** om de lijst met gebruikers weer te geven.</span><span class="sxs-lookup"><span data-stu-id="6d701-200">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6d701-202">Klik aan de bovenkant van het dialoogvenster **toevoegen** openen de **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6d701-202">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6d701-204">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="6d701-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6d701-206">a.</span><span class="sxs-lookup"><span data-stu-id="6d701-206">a.</span></span> <span data-ttu-id="6d701-207">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6d701-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6d701-208">b.</span><span class="sxs-lookup"><span data-stu-id="6d701-208">b.</span></span> <span data-ttu-id="6d701-209">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6d701-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6d701-210">c.</span><span class="sxs-lookup"><span data-stu-id="6d701-210">c.</span></span> <span data-ttu-id="6d701-211">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="6d701-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6d701-212">d.</span><span class="sxs-lookup"><span data-stu-id="6d701-212">d.</span></span> <span data-ttu-id="6d701-213">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="6d701-213">Click **Create**.</span></span> 



### <a name="creating-a-planmyleave-test-user"></a><span data-ttu-id="6d701-214">Een testgebruiker PlanMyLeave maken</span><span class="sxs-lookup"><span data-stu-id="6d701-214">Creating a PlanMyLeave test user</span></span>

<span data-ttu-id="6d701-215">Het doel van deze sectie is het maken van een gebruiker Britta Simon in PlanMyLeave genoemd.</span><span class="sxs-lookup"><span data-stu-id="6d701-215">The objective of this section is to create a user called Britta Simon in PlanMyLeave.</span></span> <span data-ttu-id="6d701-216">PlanMyLeave ondersteunt just-in-time-inrichting, dit is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="6d701-216">PlanMyLeave supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="6d701-217">Er is geen actie-item voor u in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="6d701-217">There is no action item for you in this section.</span></span> <span data-ttu-id="6d701-218">Een nieuwe gebruiker wordt gemaakt tijdens een poging tot toegang tot PlanMyLeave als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="6d701-218">A new user will be created during an attempt to access PlanMyLeave if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="6d701-219">Als u een gebruiker handmatig maken wilt, moet u contact op met [PlanMyLeave ondersteuningsteam](mailto:support@planmyleave.com).</span><span class="sxs-lookup"><span data-stu-id="6d701-219">If you need to create an user manually, you need to contact [PlanMyLeave support team](mailto:support@planmyleave.com).</span></span>



### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6d701-220">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d701-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6d701-221">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door haar toegang verlenen aan PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="6d701-221">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to PlanMyLeave.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="6d701-223">**Britta Simon om aan te wijzen PlanMyLeave, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="6d701-223">**To assign Britta Simon to PlanMyLeave, perform the following steps:**</span></span>

1. <span data-ttu-id="6d701-224">In de Azure-beheerportal, opent u de weergave toepassingen en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="6d701-224">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="6d701-226">Selecteer in de lijst met toepassingen **PlanMyLeave**.</span><span class="sxs-lookup"><span data-stu-id="6d701-226">In the applications list, select **PlanMyLeave**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_50.png) 

3. <span data-ttu-id="6d701-228">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="6d701-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="6d701-230">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="6d701-230">Click **Add** button.</span></span> <span data-ttu-id="6d701-231">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6d701-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="6d701-233">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="6d701-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6d701-234">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6d701-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6d701-235">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="6d701-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="6d701-236">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="6d701-236">Testing single sign-on</span></span>

<span data-ttu-id="6d701-237">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="6d701-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6d701-238">Als u op de tegel PlanMyLeave in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="6d701-238">When you click the PlanMyLeave tile in the Access Panel, you should get automatically signed-on to your PlanMyLeave application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="6d701-239">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="6d701-239">Additional resources</span></span>

* [<span data-ttu-id="6d701-240">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6d701-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6d701-241">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6d701-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_203.png