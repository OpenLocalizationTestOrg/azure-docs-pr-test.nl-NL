---
title: 'Zelfstudie: Azure Active Directory-integratie met RFPIO | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en RFPIO.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 87187076-7b50-4247-814f-f217b052703f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 26a8bb17dad5a01b401ce7f9b484f09822825cbf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rfpio"></a><span data-ttu-id="d2b40-103">Zelfstudie: Azure Active Directory-integratie met RFPIO</span><span class="sxs-lookup"><span data-stu-id="d2b40-103">Tutorial: Azure Active Directory integration with RFPIO</span></span>

<span data-ttu-id="d2b40-104">In deze zelfstudie leert u hoe RFPIO integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d2b40-104">In this tutorial, you learn how to integrate RFPIO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d2b40-105">RFPIO integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="d2b40-105">Integrating RFPIO with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d2b40-106">U kunt bepalen wie in Azure AD die toegang heeft tot RFPIO.</span><span class="sxs-lookup"><span data-stu-id="d2b40-106">You can control who in Azure AD who has access to RFPIO.</span></span>
- <span data-ttu-id="d2b40-107">U kunt uw gebruikers automatisch ophalen aangemeld bij RFPIO (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="d2b40-107">You can enable your users to automatically get signed-on to RFPIO (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="d2b40-108">U kunt uw accounts op één centrale locatie--de Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="d2b40-108">You can manage your accounts in one central location--the Azure portal.</span></span>

<span data-ttu-id="d2b40-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d2b40-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2b40-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d2b40-110">Prerequisites</span></span>

<span data-ttu-id="d2b40-111">Voor het configureren van Azure AD-integratie met RFPIO, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="d2b40-111">To configure Azure AD integration with RFPIO, you need the following items:</span></span>

- <span data-ttu-id="d2b40-112">Een Azure AD-abonnement.</span><span class="sxs-lookup"><span data-stu-id="d2b40-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="d2b40-113">Een RFPIO eenmalige aanmelding op ingeschakeld abonnement.</span><span class="sxs-lookup"><span data-stu-id="d2b40-113">A RFPIO single sign-on-enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="d2b40-114">Niet aanbevolen dat u een productie-omgeving voor het testen van de stappen in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="d2b40-114">We don't recommend that you use a production environment to test the steps in this tutorial.</span></span>

<span data-ttu-id="d2b40-115">Test de stappen in deze zelfstudie, volgt u deze aanbevelingen:</span><span class="sxs-lookup"><span data-stu-id="d2b40-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="d2b40-116">Gebruik uw productieomgeving tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="d2b40-116">Do not use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="d2b40-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een [proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d2b40-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d2b40-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="d2b40-118">Scenario description</span></span>
<span data-ttu-id="d2b40-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="d2b40-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d2b40-120">Het scenario dat wordt beschreven in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="d2b40-120">The scenario that's outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d2b40-121">RFPIO uit de galerie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="d2b40-121">Adding RFPIO from the gallery.</span></span>
2. <span data-ttu-id="d2b40-122">Configureren en testen van Azure AD eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="d2b40-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-rfpio-from-the-gallery"></a><span data-ttu-id="d2b40-123">RFPIO uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="d2b40-123">Add RFPIO from the gallery</span></span>
<span data-ttu-id="d2b40-124">Voor het configureren van de integratie van RFPIO in Azure AD, moet u RFPIO uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="d2b40-124">To configure the integration of RFPIO into Azure AD, you need to add RFPIO from the gallery to your list of managed SaaS apps.</span></span>

### <a name="to-add-rfpio-from-the-gallery"></a><span data-ttu-id="d2b40-125">RFPIO uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="d2b40-125">To add RFPIO from the gallery</span></span>

1. <span data-ttu-id="d2b40-126">In de  **[Azure-portal](https://portal.azure.com)**, Selecteer op het navigatiedeelvenster links de **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d2b40-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation pane, select the **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d2b40-128">Selecteer **bedrijfstoepassingen**, en selecteer vervolgens **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d2b40-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="d2b40-130">Als u wilt een nieuwe toepassing toevoegen, selecteert u de **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d2b40-130">To add a new application, select the **New application** button on the top of dialog box.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="d2b40-132">Typ in het zoekvak **RFPIO**.</span><span class="sxs-lookup"><span data-stu-id="d2b40-132">In the search box, type **RFPIO**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_search.png)

5. <span data-ttu-id="d2b40-134">Selecteer in het deelvenster resultaten **RFPIO**, en selecteer vervolgens de **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="d2b40-134">In the results panel, select **RFPIO**, and then select the **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d2b40-136">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2b40-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="d2b40-137">In deze sectie configureert en test eenmalige aanmelding Azure AD met RFPIO op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="d2b40-137">In this section, you configure and test Azure AD single sign-on with RFPIO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d2b40-138">Voor eenmalige aanmelding werkt, moet Azure AD weten wat is de relatie tussen de gebruiker die equivalent in RFPIO en een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d2b40-138">For single sign-on to work, Azure AD needs to know what the relationship is between counterpart user in RFPIO and a user in Azure AD.</span></span> <span data-ttu-id="d2b40-139">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in RFPIO tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="d2b40-139">In other words, a link relationship between an Azure AD user and the related user in RFPIO needs to be established.</span></span>

<span data-ttu-id="d2b40-140">De waarde van toewijzen in RFPIO, **gebruikersnaam** in Azure AD als de waarde van **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="d2b40-140">In RFPIO, assign the value of **user name** in Azure AD as the value of  **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d2b40-141">Om te configureren en testen van Azure AD eenmalige aanmelding met RFPIO, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="d2b40-141">To configure and test Azure AD single sign-on with RFPIO, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d2b40-142">**[Azure AD eenmalige aanmelding configureren](#configuring-azure-ad-single-sign-on)**--zodat uw gebruikers om deze functie te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d2b40-142">**[Configure Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**--to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d2b40-143">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**--voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d2b40-143">**[Create an Azure AD test user](#creating-an-azure-ad-test-user)**-- to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d2b40-144">**[Maak een testgebruiker RFPIO](#creating-a-rfpio-test-user)**  --RFPIO die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="d2b40-144">**[Create a RFPIO test user](#creating-a-rfpio-test-user)** --to have a counterpart of Britta Simon in RFPIO that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d2b40-145">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**--Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="d2b40-145">**[Assign the Azure AD test user](#assigning-the-azure-ad-test-user)**--to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d2b40-146">**[Test eenmalige aanmelding](#testing-single-sign-on)**  --controleren als de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="d2b40-146">**[Test Single Sign-On](#testing-single-sign-on)** --to verify if the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d2b40-147">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="d2b40-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d2b40-148">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing RFPIO configureren.</span><span class="sxs-lookup"><span data-stu-id="d2b40-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RFPIO application.</span></span>

<span data-ttu-id="d2b40-149">**Voor het configureren van Azure AD eenmalige aanmelding met RFPIO, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d2b40-149">**To configure Azure AD single sign-on with RFPIO, perform the following steps:**</span></span>

1. <span data-ttu-id="d2b40-150">In de Azure-portal op de **RFPIO** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="d2b40-150">In the Azure portal, on the **RFPIO** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="d2b40-152">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="d2b40-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_samlbase.png)

3. <span data-ttu-id="d2b40-154">Op de **RFPIO domein en de URL's** sectie als u wilt configureren van de toepassing in **IDP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="d2b40-154">On the **RFPIO Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url.png)

    <span data-ttu-id="d2b40-156">a.</span><span class="sxs-lookup"><span data-stu-id="d2b40-156">a.</span></span> <span data-ttu-id="d2b40-157">In de **id** textbox, typ de URL:`https://www.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="d2b40-157">In the **Identifier** textbox, type the URL: `https://www.rfpio.com`</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url1.png)

    <span data-ttu-id="d2b40-159">b.</span><span class="sxs-lookup"><span data-stu-id="d2b40-159">b.</span></span> <span data-ttu-id="d2b40-160">Controleer **weergeven geavanceerde instellingen voor URL**.</span><span class="sxs-lookup"><span data-stu-id="d2b40-160">Check **Show advanced URL settings**.</span></span>

    <span data-ttu-id="d2b40-161">c.</span><span class="sxs-lookup"><span data-stu-id="d2b40-161">c.</span></span> <span data-ttu-id="d2b40-162">In de **Relay status** textbox een tekenreekswaarde invoeren.</span><span class="sxs-lookup"><span data-stu-id="d2b40-162">In the **Relay State** textbox enter a string value.</span></span> <span data-ttu-id="d2b40-163">Neem contact op met [RFPIO ondersteuningsteam](https://www.rfpio.com/contact/) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="d2b40-163">Contact [RFPIO support team](https://www.rfpio.com/contact/) to get this value.</span></span> 

4. <span data-ttu-id="d2b40-164">Controleer **weergeven geavanceerde instellingen voor URL**.</span><span class="sxs-lookup"><span data-stu-id="d2b40-164">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="d2b40-165">Als u wilt configureren van de toepassing in **SP** modus gestart:</span><span class="sxs-lookup"><span data-stu-id="d2b40-165">If you wish to configure the application in **SP** initiated mode:</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url2.png)

    <span data-ttu-id="d2b40-167">In de **aanmelden URL** textbox, typ de URL:`https://www.app.rfpio.com`</span><span class="sxs-lookup"><span data-stu-id="d2b40-167">In the **Sign on URL** textbox, type the URL: `https://www.app.rfpio.com`</span></span>

5. <span data-ttu-id="d2b40-168">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="d2b40-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_certificate.png) 

6. <span data-ttu-id="d2b40-170">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="d2b40-170">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="d2b40-172">In een ander browservenster, meld u aan bij de **RFPIO** website als beheerder.</span><span class="sxs-lookup"><span data-stu-id="d2b40-172">In a different web browser window, login to the **RFPIO** website as an administrator.</span></span>

8. <span data-ttu-id="d2b40-173">Klik op de vervolgkeuzelijst van de linkerhoek onder.</span><span class="sxs-lookup"><span data-stu-id="d2b40-173">Click on the bottom left corner dropdown.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/app1.png)

9. <span data-ttu-id="d2b40-175">Klik op de **organisatie-instellingen**.</span><span class="sxs-lookup"><span data-stu-id="d2b40-175">Click on the **Organization Settings**.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/app2.png)

10. <span data-ttu-id="d2b40-177">Klik op de **functies & integratie**.</span><span class="sxs-lookup"><span data-stu-id="d2b40-177">Click on the **FEATURES & INTEGRATION**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/app4.png)

11. <span data-ttu-id="d2b40-179">In de **SAML SSO configuratie** klikt u op **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="d2b40-179">In the **SAML SSO Configuration** Click **Edit**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/app3.png)

12. <span data-ttu-id="d2b40-181">In deze sectie voert u volgende acties:</span><span class="sxs-lookup"><span data-stu-id="d2b40-181">In this Section perform following actions:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/app5.png)
    
    <span data-ttu-id="d2b40-183">a.</span><span class="sxs-lookup"><span data-stu-id="d2b40-183">a.</span></span> <span data-ttu-id="d2b40-184">Kopieer de inhoud van de **gedownload van metagegevens-XML** en plak deze in de **identiteit configuratie** veld.</span><span class="sxs-lookup"><span data-stu-id="d2b40-184">Copy the content of the **Downloaded Metadata XML** and paste it into the **identity configuration** field.</span></span>

    > [!NOTE]
    ><span data-ttu-id="d2b40-185">Kopiëren van de inhoud van gedownload **Metadata XML** gebruik **Kladblok ++** of de juiste **XML-Editor**.</span><span class="sxs-lookup"><span data-stu-id="d2b40-185">To copy the content of downloaded **Metadata XML** Use **Notepad++** or proper **XML Editor**.</span></span> 

    <span data-ttu-id="d2b40-186">b.</span><span class="sxs-lookup"><span data-stu-id="d2b40-186">b.</span></span> <span data-ttu-id="d2b40-187">Klik op **valideren**.</span><span class="sxs-lookup"><span data-stu-id="d2b40-187">Click **Validate**.</span></span>

    <span data-ttu-id="d2b40-188">c.</span><span class="sxs-lookup"><span data-stu-id="d2b40-188">c.</span></span> <span data-ttu-id="d2b40-189">Wanneer u op **valideren**, spiegelen **SAML(Enabled)** op on.</span><span class="sxs-lookup"><span data-stu-id="d2b40-189">After Clicking **Validate**, Flip **SAML(Enabled)** to on.</span></span>

    <span data-ttu-id="d2b40-190">d.</span><span class="sxs-lookup"><span data-stu-id="d2b40-190">d.</span></span> <span data-ttu-id="d2b40-191">Klik op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="d2b40-191">Click **Submit**.</span></span>

> [!TIP]
> <span data-ttu-id="d2b40-192">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="d2b40-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d2b40-193">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="d2b40-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d2b40-194">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d2b40-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d2b40-195">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="d2b40-195">Create an Azure AD test user</span></span>
<span data-ttu-id="d2b40-196">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="d2b40-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="d2b40-198">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d2b40-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d2b40-199">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="d2b40-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-rfpio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d2b40-201">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="d2b40-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-rfpio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d2b40-203">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d2b40-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-rfpio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d2b40-205">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="d2b40-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-rfpio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d2b40-207">a.</span><span class="sxs-lookup"><span data-stu-id="d2b40-207">a.</span></span> <span data-ttu-id="d2b40-208">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d2b40-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d2b40-209">b.</span><span class="sxs-lookup"><span data-stu-id="d2b40-209">b.</span></span> <span data-ttu-id="d2b40-210">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d2b40-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d2b40-211">c.</span><span class="sxs-lookup"><span data-stu-id="d2b40-211">c.</span></span> <span data-ttu-id="d2b40-212">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="d2b40-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d2b40-213">d.</span><span class="sxs-lookup"><span data-stu-id="d2b40-213">d.</span></span> <span data-ttu-id="d2b40-214">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="d2b40-214">Click **Create**.</span></span>
 
### <a name="create-a-rfpio-test-user"></a><span data-ttu-id="d2b40-215">Een testgebruiker RFPIO maken</span><span class="sxs-lookup"><span data-stu-id="d2b40-215">Create a RFPIO test user</span></span>

<span data-ttu-id="d2b40-216">Om Azure AD-gebruikers zich aanmelden bij RFPIO, moeten ze worden ingericht in RFPIO.</span><span class="sxs-lookup"><span data-stu-id="d2b40-216">To enable Azure AD users to log in to RFPIO, they must be provisioned into RFPIO.</span></span>  
<span data-ttu-id="d2b40-217">In het geval van RFPIO is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="d2b40-217">In the case of RFPIO, provisioning is a manual task.</span></span>

<span data-ttu-id="d2b40-218">**Voor het inrichten van een gebruikersaccount, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d2b40-218">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="d2b40-219">Meld u aan bij uw bedrijf RFPIO site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="d2b40-219">Log in to your RFPIO company site as an administrator.</span></span>

2. <span data-ttu-id="d2b40-220">Klik op de vervolgkeuzelijst van de linkerhoek onder.</span><span class="sxs-lookup"><span data-stu-id="d2b40-220">Click on the bottom left corner dropdown.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/app1.png)

3. <span data-ttu-id="d2b40-222">Klik op de **organisatie-instellingen**.</span><span class="sxs-lookup"><span data-stu-id="d2b40-222">Click on the **Organization Settings**.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/app2.png)

4. <span data-ttu-id="d2b40-224">Klik op **TEAMLEDEN**.</span><span class="sxs-lookup"><span data-stu-id="d2b40-224">Click **TEAM MEMBERS**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/app6.png)

5. <span data-ttu-id="d2b40-226">Klik op **leden toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="d2b40-226">Click on **ADD MEMBERS**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/app7.png)

6. <span data-ttu-id="d2b40-228">In de **nieuwe leden toevoegen** sectie.</span><span class="sxs-lookup"><span data-stu-id="d2b40-228">In the **Add New Members** section.</span></span> <span data-ttu-id="d2b40-229">Voer de volgende acties:</span><span class="sxs-lookup"><span data-stu-id="d2b40-229">Perform following actions:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/app8.png)

    <span data-ttu-id="d2b40-231">a.</span><span class="sxs-lookup"><span data-stu-id="d2b40-231">a.</span></span> <span data-ttu-id="d2b40-232">Voer **e-mailadres** in de **Voer één e-mailadres per regel** veld.</span><span class="sxs-lookup"><span data-stu-id="d2b40-232">Enter **Email address** in the **Enter one email per line** field.</span></span>

    <span data-ttu-id="d2b40-233">b.</span><span class="sxs-lookup"><span data-stu-id="d2b40-233">b.</span></span> <span data-ttu-id="d2b40-234">Selecteer Plese **rol** volgens uw vereisten.</span><span class="sxs-lookup"><span data-stu-id="d2b40-234">Plese select **Role** according your requirements.</span></span>

    <span data-ttu-id="d2b40-235">c.</span><span class="sxs-lookup"><span data-stu-id="d2b40-235">c.</span></span> <span data-ttu-id="d2b40-236">Klik op **leden toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="d2b40-236">Click **ADD MEMBERS**.</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="d2b40-237">De houder van Azure Active Directory-account ontvangt een e-mailbericht en volgt een koppeling om hun account te bevestigen voordat deze geactiveerd wordt.</span><span class="sxs-lookup"><span data-stu-id="d2b40-237">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="d2b40-238">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="d2b40-238">Assign the Azure AD test user</span></span>

<span data-ttu-id="d2b40-239">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan RFPIO.</span><span class="sxs-lookup"><span data-stu-id="d2b40-239">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RFPIO.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="d2b40-241">**Britta Simon om aan te wijzen RFPIO, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="d2b40-241">**To assign Britta Simon to RFPIO, perform the following steps:**</span></span>

1. <span data-ttu-id="d2b40-242">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="d2b40-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="d2b40-244">Selecteer in de lijst met toepassingen **RFPIO**.</span><span class="sxs-lookup"><span data-stu-id="d2b40-244">In the applications list, select **RFPIO**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_app.png) 

3. <span data-ttu-id="d2b40-246">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="d2b40-246">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="d2b40-248">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="d2b40-248">Click **Add** button.</span></span> <span data-ttu-id="d2b40-249">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d2b40-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="d2b40-251">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="d2b40-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d2b40-252">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d2b40-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d2b40-253">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d2b40-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d2b40-254">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="d2b40-254">Test single sign-on</span></span>

<span data-ttu-id="d2b40-255">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie testen met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="d2b40-255">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="d2b40-256">Als u op de tegel RFPIO in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing RFPIO.</span><span class="sxs-lookup"><span data-stu-id="d2b40-256">When you click the RFPIO tile in the Access Panel, you should get automatically signed-on to your RFPIO application.</span></span>
<span data-ttu-id="d2b40-257">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d2b40-257">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d2b40-258">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="d2b40-258">Additional resources</span></span>

* [<span data-ttu-id="d2b40-259">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d2b40-259">List of tutorials about how to integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d2b40-260">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d2b40-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_203.png

