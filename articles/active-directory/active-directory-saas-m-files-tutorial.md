---
title: 'Zelfstudie: Azure Active Directory-integratie met M-bestanden | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en M-bestanden.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4536fd49-3a65-4cff-9620-860904f726d0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 0f2682cf7cd3e11a5a7156938fbe9d4c7f541312
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-m-files"></a><span data-ttu-id="39bef-103">Zelfstudie: Azure Active Directory-integratie met M-bestanden</span><span class="sxs-lookup"><span data-stu-id="39bef-103">Tutorial: Azure Active Directory integration with M-Files</span></span>

<span data-ttu-id="39bef-104">In deze zelfstudie leert u hoe M bestanden integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="39bef-104">In this tutorial, you learn how to integrate M-Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="39bef-105">M-bestanden worden geïntegreerd met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="39bef-105">Integrating M-Files with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="39bef-106">U kunt beheren in Azure AD die toegang tot M-bestanden heeft</span><span class="sxs-lookup"><span data-stu-id="39bef-106">You can control in Azure AD who has access to M-Files</span></span>
- <span data-ttu-id="39bef-107">U kunt uw gebruikers automatisch ophalen aangemeld bij M-bestanden (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="39bef-107">You can enable your users to automatically get signed-on to M-Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="39bef-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="39bef-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="39bef-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="39bef-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="39bef-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="39bef-110">Prerequisites</span></span>

<span data-ttu-id="39bef-111">Voor het configureren van Azure AD-integratie met M-bestanden, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="39bef-111">To configure Azure AD integration with M-Files, you need the following items:</span></span>

- <span data-ttu-id="39bef-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="39bef-112">An Azure AD subscription</span></span>
- <span data-ttu-id="39bef-113">Een M bestanden eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="39bef-113">A M-Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="39bef-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="39bef-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="39bef-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="39bef-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="39bef-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="39bef-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="39bef-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="39bef-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="39bef-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="39bef-118">Scenario description</span></span>
<span data-ttu-id="39bef-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="39bef-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="39bef-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="39bef-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="39bef-121">M-bestanden uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="39bef-121">Adding M-Files from the gallery</span></span>
2. <span data-ttu-id="39bef-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="39bef-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-m-files-from-the-gallery"></a><span data-ttu-id="39bef-123">M-bestanden uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="39bef-123">Adding M-Files from the gallery</span></span>
<span data-ttu-id="39bef-124">Voor het configureren van de integratie van M-bestanden in Azure AD, moet u M-bestanden uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="39bef-124">To configure the integration of M-Files into Azure AD, you need to add M-Files from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="39bef-125">**Als u wilt toevoegen M-bestanden uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="39bef-125">**To add M-Files from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="39bef-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="39bef-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="39bef-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="39bef-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="39bef-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="39bef-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="39bef-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="39bef-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="39bef-133">Typ in het zoekvak **M bestanden**.</span><span class="sxs-lookup"><span data-stu-id="39bef-133">In the search box, type **M-Files**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_search.png)

5. <span data-ttu-id="39bef-135">Selecteer in het deelvenster resultaten **M bestanden**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="39bef-135">In the results panel, select **M-Files**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="39bef-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="39bef-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="39bef-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met M-bestanden op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="39bef-138">In this section, you configure and test Azure AD single sign-on with M-Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="39bef-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in de M-bestanden is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="39bef-139">For single sign-on to work, Azure AD needs to know what the counterpart user in M-Files is to a user in Azure AD.</span></span> <span data-ttu-id="39bef-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in M bestanden worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="39bef-140">In other words, a link relationship between an Azure AD user and the related user in M-Files needs to be established.</span></span>

<span data-ttu-id="39bef-141">In de M-bestanden, wijs de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="39bef-141">In M-Files, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="39bef-142">Om te configureren en testen van Azure AD eenmalige aanmelding met M-bestanden, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="39bef-142">To configure and test Azure AD single sign-on with M-Files, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="39bef-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="39bef-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="39bef-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="39bef-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="39bef-145">**[Maken van een testgebruiker M bestanden](#creating-a-m-files-test-user)**  - hebben een equivalent van Britta Simon in M-bestanden dat is gekoppeld aan de Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="39bef-145">**[Creating a M-Files test user](#creating-a-m-files-test-user)** - to have a counterpart of Britta Simon in M-Files that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="39bef-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="39bef-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="39bef-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="39bef-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="39bef-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="39bef-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="39bef-149">In deze sectie maakt u Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw toepassing M-bestanden.</span><span class="sxs-lookup"><span data-stu-id="39bef-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your M-Files application.</span></span>

<span data-ttu-id="39bef-150">**Voor het configureren van Azure AD eenmalige aanmelding met M-bestanden, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="39bef-150">**To configure Azure AD single sign-on with M-Files, perform the following steps:**</span></span>

1. <span data-ttu-id="39bef-151">In de Azure-portal op de **M bestanden** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="39bef-151">In the Azure portal, on the **M-Files** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="39bef-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="39bef-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_samlbase.png)

3. <span data-ttu-id="39bef-155">Op de **M bestanden domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="39bef-155">On the **M-Files Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_url.png)

    <span data-ttu-id="39bef-157">a.</span><span class="sxs-lookup"><span data-stu-id="39bef-157">a.</span></span> <span data-ttu-id="39bef-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span><span class="sxs-lookup"><span data-stu-id="39bef-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span></span>

    <span data-ttu-id="39bef-159">b.</span><span class="sxs-lookup"><span data-stu-id="39bef-159">b.</span></span> <span data-ttu-id="39bef-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<tenantname>.cloudvault.m-files.com`</span><span class="sxs-lookup"><span data-stu-id="39bef-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.cloudvault.m-files.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="39bef-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="39bef-161">These values are not real.</span></span> <span data-ttu-id="39bef-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="39bef-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="39bef-163">Neem contact op met [M bestanden Client ondersteuningsteam](mailto:support@m-files.com) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="39bef-163">Contact [M-Files Client support team](mailto:support@m-files.com) to get these values.</span></span> 
 
4. <span data-ttu-id="39bef-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="39bef-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_certificate.png) 

5. <span data-ttu-id="39bef-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="39bef-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-m-files-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="39bef-168">Als u eenmalige aanmelding die zijn geconfigureerd voor uw toepassing, neem contact op met [M bestanden ondersteuningsteam](mailto:support@m-files.com) en geeft u de gedownloade metagegevens.</span><span class="sxs-lookup"><span data-stu-id="39bef-168">To get SSO configured for your application, contact [M-Files support team](mailto:support@m-files.com) and provide them the downloaded Metadata.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="39bef-169">Voer de volgende stappen uit als u wilt configureren van eenmalige aanmelding voor u bureaubladtoepassing M-bestand.</span><span class="sxs-lookup"><span data-stu-id="39bef-169">Follow the next steps if you want to configure SSO for you M-File desktop application.</span></span> <span data-ttu-id="39bef-170">Er zijn geen extra stappen vereist als u alleen wilt eenmalige aanmelding configureren voor de webversie M-bestanden.</span><span class="sxs-lookup"><span data-stu-id="39bef-170">No extra steps are required if you only want to configure SSO for M-Files web version.</span></span>  

7. <span data-ttu-id="39bef-171">Volg de volgende stappen om de M-bestand bureaublad toepassing configureren voor eenmalige aanmelding met Azure AD inschakelen.</span><span class="sxs-lookup"><span data-stu-id="39bef-171">Follow the next steps to configure the M-File desktop application to enable SSO with Azure AD.</span></span> <span data-ttu-id="39bef-172">M-om bestanden te downloaden, gaat u naar [M-bestanden downloaden](https://www.m-files.com/en/download-latest-version) pagina.</span><span class="sxs-lookup"><span data-stu-id="39bef-172">To download M-Files, go to [M-Files download](https://www.m-files.com/en/download-latest-version) page.</span></span>

8. <span data-ttu-id="39bef-173">Open de **M bestanden bureaublad instellingen** venster.</span><span class="sxs-lookup"><span data-stu-id="39bef-173">Open the **M-Files Desktop Settings** window.</span></span> <span data-ttu-id="39bef-174">Klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="39bef-174">Then, click **Add**.</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_10.png)

9. <span data-ttu-id="39bef-176">Op de **Document kluis verbindingseigenschappen** venster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="39bef-176">On the **Document Vault Connection Properties** window, perform the following steps:</span></span>
   
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_11.png)  

    <span data-ttu-id="39bef-178">Sectie type, de waarden als volgt onder de Server:</span><span class="sxs-lookup"><span data-stu-id="39bef-178">Under the Server section type, the values as follows:</span></span>  

    <span data-ttu-id="39bef-179">a.</span><span class="sxs-lookup"><span data-stu-id="39bef-179">a.</span></span> <span data-ttu-id="39bef-180">Voor **naam**, type `<tenant-name>.cloudvault.m-files.com`.</span><span class="sxs-lookup"><span data-stu-id="39bef-180">For **Name**, type `<tenant-name>.cloudvault.m-files.com`.</span></span> 
 
    <span data-ttu-id="39bef-181">b.</span><span class="sxs-lookup"><span data-stu-id="39bef-181">b.</span></span> <span data-ttu-id="39bef-182">Voor **poortnummer**, type **4466**.</span><span class="sxs-lookup"><span data-stu-id="39bef-182">For **Port Number**, type **4466**.</span></span> 

    <span data-ttu-id="39bef-183">c.</span><span class="sxs-lookup"><span data-stu-id="39bef-183">c.</span></span> <span data-ttu-id="39bef-184">Voor **Protocol**, selecteer **HTTPS**.</span><span class="sxs-lookup"><span data-stu-id="39bef-184">For **Protocol**, select **HTTPS**.</span></span> 

    <span data-ttu-id="39bef-185">d.</span><span class="sxs-lookup"><span data-stu-id="39bef-185">d.</span></span> <span data-ttu-id="39bef-186">In de **verificatie** optie **specifieke Windows-gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="39bef-186">In the **Authentication** field, select **Specific Windows user**.</span></span> <span data-ttu-id="39bef-187">Vervolgens wordt u gevraagd met een pagina ondertekenen.</span><span class="sxs-lookup"><span data-stu-id="39bef-187">Then, you are prompted with a signing page.</span></span> <span data-ttu-id="39bef-188">Voeg in uw Azure AD-referenties.</span><span class="sxs-lookup"><span data-stu-id="39bef-188">Insert your Azure AD credentials.</span></span> 

    <span data-ttu-id="39bef-189">e.</span><span class="sxs-lookup"><span data-stu-id="39bef-189">e.</span></span> <span data-ttu-id="39bef-190">Voor de **kluis op Server**, selecteert u de betreffende kluis op de server.</span><span class="sxs-lookup"><span data-stu-id="39bef-190">For the **Vault on Server**,  select the corresponding vault on server.</span></span>
 
    <span data-ttu-id="39bef-191">f.</span><span class="sxs-lookup"><span data-stu-id="39bef-191">f.</span></span> <span data-ttu-id="39bef-192">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="39bef-192">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="39bef-193">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="39bef-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="39bef-194">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="39bef-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="39bef-195">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="39bef-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="39bef-196">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="39bef-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="39bef-197">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="39bef-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="39bef-199">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="39bef-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="39bef-200">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="39bef-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-m-files-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="39bef-202">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="39bef-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-m-files-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="39bef-204">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="39bef-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-m-files-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="39bef-206">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="39bef-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-m-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="39bef-208">a.</span><span class="sxs-lookup"><span data-stu-id="39bef-208">a.</span></span> <span data-ttu-id="39bef-209">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="39bef-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="39bef-210">b.</span><span class="sxs-lookup"><span data-stu-id="39bef-210">b.</span></span> <span data-ttu-id="39bef-211">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="39bef-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="39bef-212">c.</span><span class="sxs-lookup"><span data-stu-id="39bef-212">c.</span></span> <span data-ttu-id="39bef-213">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="39bef-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="39bef-214">d.</span><span class="sxs-lookup"><span data-stu-id="39bef-214">d.</span></span> <span data-ttu-id="39bef-215">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="39bef-215">Click **Create**.</span></span>
 
### <a name="creating-a-m-files-test-user"></a><span data-ttu-id="39bef-216">Een testgebruiker M-bestanden maken</span><span class="sxs-lookup"><span data-stu-id="39bef-216">Creating a M-Files test user</span></span>

<span data-ttu-id="39bef-217">Het doel van deze sectie is het maken van een gebruiker Britta Simon aangeroepen in M-bestanden.</span><span class="sxs-lookup"><span data-stu-id="39bef-217">The objective of this section is to create a user called Britta Simon in M-Files.</span></span> <span data-ttu-id="39bef-218">Werken met [M bestanden ondersteuningsteam](mailto:support@m-files.com) om toe te voegen de gebruikers in de M-bestanden.</span><span class="sxs-lookup"><span data-stu-id="39bef-218">Work with  [M-Files support team](mailto:support@m-files.com) to add the users in the M-Files.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="39bef-219">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="39bef-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="39bef-220">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding toegang verleent tot M-bestanden gebruiken.</span><span class="sxs-lookup"><span data-stu-id="39bef-220">In this section, you enable Britta Simon to use Azure single sign-on by granting access to M-Files.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="39bef-222">**Britta Simon om aan te wijzen M-bestanden, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="39bef-222">**To assign Britta Simon to M-Files, perform the following steps:**</span></span>

1. <span data-ttu-id="39bef-223">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="39bef-223">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="39bef-225">Selecteer in de lijst met toepassingen **M bestanden**.</span><span class="sxs-lookup"><span data-stu-id="39bef-225">In the applications list, select **M-Files**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_app.png) 

3. <span data-ttu-id="39bef-227">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="39bef-227">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="39bef-229">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="39bef-229">Click **Add** button.</span></span> <span data-ttu-id="39bef-230">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="39bef-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="39bef-232">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="39bef-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="39bef-233">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="39bef-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="39bef-234">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="39bef-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="39bef-235">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="39bef-235">Testing single sign-on</span></span>

<span data-ttu-id="39bef-236">Het doel van deze sectie is het testen van uw Azure AD SSO-configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="39bef-236">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="39bef-237">Als u op de tegel M-bestanden in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing M-bestanden.</span><span class="sxs-lookup"><span data-stu-id="39bef-237">When you click the M-Files tile in the Access Panel, you should get automatically signed-on to your M-Files application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="39bef-238">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="39bef-238">Additional resources</span></span>

* [<span data-ttu-id="39bef-239">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="39bef-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="39bef-240">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="39bef-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_203.png

