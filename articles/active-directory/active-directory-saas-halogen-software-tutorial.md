---
title: 'Zelfstudie: Azure Active Directory-integratie met halogeen Software | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en halogeen Software.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ca2298d-9a0c-4f14-925c-fa23f2659d28
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: e09fa93038965e4880a23002bac6917ad2a077f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halogen-software"></a><span data-ttu-id="b0b2e-103">Zelfstudie: Azure Active Directory-integratie met halogeen Software</span><span class="sxs-lookup"><span data-stu-id="b0b2e-103">Tutorial: Azure Active Directory integration with Halogen Software</span></span>

<span data-ttu-id="b0b2e-104">In deze zelfstudie leert u hoe halogeen Software integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b0b2e-104">In this tutorial, you learn how to integrate Halogen Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b0b2e-105">Halogeen Software integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="b0b2e-105">Integrating Halogen Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b0b2e-106">U kunt beheren in Azure AD die toegang tot halogeen Software heeft</span><span class="sxs-lookup"><span data-stu-id="b0b2e-106">You can control in Azure AD who has access to Halogen Software</span></span>
- <span data-ttu-id="b0b2e-107">U kunt uw gebruikers automatisch ophalen aangemeld bij halogeen Software (Single Sign-On) inschakelen met hun Azure AD-accounts</span><span class="sxs-lookup"><span data-stu-id="b0b2e-107">You can enable your users to automatically get signed-on to Halogen Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b0b2e-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="b0b2e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b0b2e-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b0b2e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b0b2e-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b0b2e-110">Prerequisites</span></span>

<span data-ttu-id="b0b2e-111">Voor het configureren van Azure AD-integratie met halogeen Software, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="b0b2e-111">To configure Azure AD integration with Halogen Software, you need the following items:</span></span>

- <span data-ttu-id="b0b2e-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="b0b2e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b0b2e-113">Een halogeen Software eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="b0b2e-113">A Halogen Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b0b2e-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b0b2e-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="b0b2e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b0b2e-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b0b2e-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b0b2e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b0b2e-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="b0b2e-118">Scenario description</span></span>

<span data-ttu-id="b0b2e-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b0b2e-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="b0b2e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b0b2e-121">Halogeen Software uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="b0b2e-121">Adding Halogen Software from the gallery</span></span>
2. <span data-ttu-id="b0b2e-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b0b2e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-halogen-software-from-the-gallery"></a><span data-ttu-id="b0b2e-123">Halogeen Software uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="b0b2e-123">Adding Halogen Software from the gallery</span></span>

<span data-ttu-id="b0b2e-124">Voor het configureren van de integratie van halogeen Software in Azure AD, moet u halogeen Software uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-124">To configure the integration of Halogen Software into Azure AD, you need to add Halogen Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b0b2e-125">**Als u wilt toevoegen halogeen Software uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b0b2e-125">**To add Halogen Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b0b2e-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b0b2e-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b0b2e-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="b0b2e-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="b0b2e-133">Typ in het zoekvak **halogeen Software**.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-133">In the search box, type **Halogen Software**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_search.png)

5. <span data-ttu-id="b0b2e-135">Selecteer in het deelvenster resultaten **halogeen Software**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-135">In the results panel, select **Halogen Software**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b0b2e-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b0b2e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b0b2e-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met halogeen Software op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-138">In this section, you configure and test Azure AD single sign-on with Halogen Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b0b2e-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in halogeen Software is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Halogen Software is to a user in Azure AD.</span></span> <span data-ttu-id="b0b2e-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in halogeen Software worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-140">In other words, a link relationship between an Azure AD user and the related user in Halogen Software needs to be established.</span></span>

<span data-ttu-id="b0b2e-141">Wijs in halogeen Software, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-141">In Halogen Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b0b2e-142">Om te configureren en testen van Azure AD eenmalige aanmelding met halogeen Software, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="b0b2e-142">To configure and test Azure AD single sign-on with Halogen Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b0b2e-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b0b2e-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b0b2e-145">**[Maken van een testgebruiker halogeen Software](#creating-a-halogen-software-test-user)**  - halogeen-Software die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-145">**[Creating a Halogen Software test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in Halogen Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b0b2e-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b0b2e-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b0b2e-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="b0b2e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b0b2e-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing halogeen Software configureren.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Halogen Software application.</span></span>

<span data-ttu-id="b0b2e-150">**Voor het configureren van Azure AD eenmalige aanmelding met halogeen Software, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b0b2e-150">**To configure Azure AD single sign-on with Halogen Software, perform the following steps:**</span></span>

1. <span data-ttu-id="b0b2e-151">In de Azure-portal op de **halogeen Software** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-151">In the Azure portal, on the **Halogen Software** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="b0b2e-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_samlbase.png)

3. <span data-ttu-id="b0b2e-155">Op de **halogeen Software domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b0b2e-155">On the **Halogen Software Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_url.png)

    <span data-ttu-id="b0b2e-157">a.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-157">a.</span></span> <span data-ttu-id="b0b2e-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="b0b2e-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://global.hgncloud.com/<companyname>`</span></span>

    <span data-ttu-id="b0b2e-159">b.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-159">b.</span></span> <span data-ttu-id="b0b2e-160">In de **id** textbox, typ een URL met het volgende patroon volgen: `https://global.halogensoftware.com/<companyname>`,`https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="b0b2e-160">In the **Identifier** textbox, type a URL using the following pattern: `https://global.halogensoftware.com/<companyname>`, `https://global.hgncloud.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b0b2e-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-161">These values are not real.</span></span> <span data-ttu-id="b0b2e-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b0b2e-163">Neem contact op met [halogeen Software Client ondersteuningsteam](https://support.halogensoftware.com/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-163">Contact [Halogen Software Client support team](https://support.halogensoftware.com/) to get these values.</span></span> 
 


4. <span data-ttu-id="b0b2e-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_certificate.png) 

5. <span data-ttu-id="b0b2e-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-halogen-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b0b2e-168">In een ander browservenster aanmelding bij uw **halogeen Software** toepassing als beheerder.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-168">In a different browser window, sign-on to your **Halogen Software** application as an administrator.</span></span>

7. <span data-ttu-id="b0b2e-169">Klik op de **opties** tabblad.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-169">Click the **Options** tab.</span></span> 
   
    ![Wat is Azure AD Connect?][12]

8. <span data-ttu-id="b0b2e-171">Klik in het navigatiedeelvenster links op **SAML-configuratie**.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-171">In the left navigation pane, click **SAML Configuration**.</span></span> 
   
    ![Wat is Azure AD Connect?][13]

9. <span data-ttu-id="b0b2e-173">Op de **SAML-configuratie** pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b0b2e-173">On the **SAML Configuration** page, perform the following steps:</span></span> 

    ![Wat is Azure AD Connect?][14]

     <span data-ttu-id="b0b2e-175">a.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-175">a.</span></span> <span data-ttu-id="b0b2e-176">Als **unieke id**, selecteer **NameID**.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-176">As **Unique Identifier**, select **NameID**.</span></span>

     <span data-ttu-id="b0b2e-177">b.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-177">b.</span></span> <span data-ttu-id="b0b2e-178">Als **unieke id gerelateerd aan**, selecteer **gebruikersnaam**.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-178">As **Unique Identifier Maps To**, select **Username**.</span></span>
  
     <span data-ttu-id="b0b2e-179">c.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-179">c.</span></span> <span data-ttu-id="b0b2e-180">Als u wilt uw van het gedownloade metagegevensbestand uploadt, klikt u op **Bladeren** om het bestand te selecteren en vervolgens **-bestand uploaden**.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-180">To upload your downloaded metadata file, click **Browse** to select the file, and then **Upload File**.</span></span>
 
     <span data-ttu-id="b0b2e-181">d.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-181">d.</span></span> <span data-ttu-id="b0b2e-182">Om de configuratie te testen, klikt u op **uitvoeren testen**.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-182">To test the configuration, click **Run Test**.</span></span> 
    
    >[!NOTE]
    ><span data-ttu-id="b0b2e-183">U moet wachten op het bericht '*de SAML-test is voltooid. Sluit dit venster*'.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-183">You need to wait for the message "*The SAML test is complete. Please close this window*".</span></span> <span data-ttu-id="b0b2e-184">Sluit het browservenster is geopend.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-184">Then, close the opened browser window.</span></span> <span data-ttu-id="b0b2e-185">De **SAML inschakelen** selectievakje is alleen ingeschakeld als de test is voltooid.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-185">The **Enable SAML** checkbox is only enabled if the test has been completed.</span></span> 
     
     <span data-ttu-id="b0b2e-186">e.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-186">e.</span></span> <span data-ttu-id="b0b2e-187">Selecteer **SAML inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-187">Select **Enable SAML**.</span></span>
    
     <span data-ttu-id="b0b2e-188">f.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-188">f.</span></span> <span data-ttu-id="b0b2e-189">Klik op **wijzigingen opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-189">Click **Save Changes**.</span></span> 

> [!TIP]
> <span data-ttu-id="b0b2e-190">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="b0b2e-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b0b2e-191">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b0b2e-192">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b0b2e-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b0b2e-193">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="b0b2e-193">Creating an Azure AD test user</span></span>

<span data-ttu-id="b0b2e-194">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="b0b2e-196">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b0b2e-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b0b2e-197">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b0b2e-199">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b0b2e-201">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b0b2e-203">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b0b2e-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b0b2e-205">a.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-205">a.</span></span> <span data-ttu-id="b0b2e-206">In de **naam** textbox typenaam als **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-206">In the **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="b0b2e-207">b.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-207">b.</span></span> <span data-ttu-id="b0b2e-208">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b0b2e-209">c.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-209">c.</span></span> <span data-ttu-id="b0b2e-210">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b0b2e-211">d.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-211">d.</span></span> <span data-ttu-id="b0b2e-212">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-212">Click **Create**.</span></span>
 
### <a name="creating-a-halogen-software-test-user"></a><span data-ttu-id="b0b2e-213">Een testgebruiker halogeen Software maken</span><span class="sxs-lookup"><span data-stu-id="b0b2e-213">Creating a Halogen Software test user</span></span>

<span data-ttu-id="b0b2e-214">Het doel van deze sectie is het maken van een gebruiker Britta Simon aangeroepen in halogeen Software.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-214">The objective of this section is to create a user called Britta Simon in Halogen Software.</span></span>

<span data-ttu-id="b0b2e-215">**Voer de volgende stappen uit voor het maken van een gebruiker Britta Simon aangeroepen in halogeen Software:**</span><span class="sxs-lookup"><span data-stu-id="b0b2e-215">**To create a user called Britta Simon in Halogen Software, perform the following steps:**</span></span>

1. <span data-ttu-id="b0b2e-216">Meld u aan bij uw **halogeen Software** toepassing als beheerder.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-216">Sign on to your **Halogen Software** application as an administrator.</span></span>

2. <span data-ttu-id="b0b2e-217">Klik op de **gebruiker Center** tabblad en klik vervolgens op **gebruiker maken**.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-217">Click the **User Center** tab, and then click **Create User**.</span></span>
   
    ![Wat is Azure AD Connect?][300]  

3. <span data-ttu-id="b0b2e-219">Op de **nieuwe gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b0b2e-219">On the **New User** dialog page, perform the following steps:</span></span>
   
    ![Wat is Azure AD Connect?][301]

    <span data-ttu-id="b0b2e-221">a.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-221">a.</span></span> <span data-ttu-id="b0b2e-222">In de **voornaam** textbox type voornaam van de gebruiker zoals **Britta**.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-222">In the **First Name** textbox, type first name of the user like **Britta**.</span></span>
    
    <span data-ttu-id="b0b2e-223">b.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-223">b.</span></span> <span data-ttu-id="b0b2e-224">In de **achternaam** textbox type achternaam van de gebruiker zoals **Simon**.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-224">In the **Last Name** textbox, type last name of the user like **Simon**.</span></span> 

    <span data-ttu-id="b0b2e-225">c.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-225">c.</span></span> <span data-ttu-id="b0b2e-226">In de **gebruikersnaam** textbox type **Britta Simon**, de gebruikersnaam, zoals in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-226">In the **Username** textbox, type **Britta Simon**, the user name as in the Azure portal.</span></span>

    <span data-ttu-id="b0b2e-227">d.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-227">d.</span></span> <span data-ttu-id="b0b2e-228">In de **wachtwoord** textbox, typ een wachtwoord voor Britta.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-228">In the **Password** textbox, type a password for Britta.</span></span>
    
    <span data-ttu-id="b0b2e-229">e.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-229">e.</span></span> <span data-ttu-id="b0b2e-230">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-230">Click **Save**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b0b2e-231">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0b2e-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b0b2e-232">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding toegang verleent tot halogeen Software gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Halogen Software.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="b0b2e-234">**Britta Simon om aan te wijzen halogeen Software, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b0b2e-234">**To assign Britta Simon to Halogen Software, perform the following steps:**</span></span>

1. <span data-ttu-id="b0b2e-235">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="b0b2e-237">Selecteer in de lijst met toepassingen **halogeen Software**.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-237">In the applications list, select **Halogen Software**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_app.png) 

3. <span data-ttu-id="b0b2e-239">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="b0b2e-241">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-241">Click **Add** button.</span></span> <span data-ttu-id="b0b2e-242">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="b0b2e-244">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b0b2e-245">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b0b2e-246">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b0b2e-247">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b0b2e-247">Testing single sign-on</span></span>

<span data-ttu-id="b0b2e-248">Het doel van deze sectie is het testen van uw Azure AD SSO-configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-248">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="b0b2e-249">Als u op de tegel halogeen Software in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing halogeen Software.</span><span class="sxs-lookup"><span data-stu-id="b0b2e-249">When you click the Halogen Software tile in the Access Panel, you should get automatically signed-on to your Halogen Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b0b2e-250">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="b0b2e-250">Additional resources</span></span>

* [<span data-ttu-id="b0b2e-251">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b0b2e-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b0b2e-252">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b0b2e-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_12.png

[13]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_13.png

[14]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_14.png

[100]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_203.png

[300]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_300.png

[301]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_301.png
