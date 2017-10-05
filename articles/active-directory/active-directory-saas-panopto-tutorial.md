---
title: 'Zelfstudie: Azure Active Directory-integratie met Panopto | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Panopto.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 89c88e23-93ce-4970-9baa-1104c4e8fe4a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 725fba1227cfc9c4850f9e2d6fd0b13e88eafa20
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panopto"></a><span data-ttu-id="3cca4-103">Zelfstudie: Azure Active Directory-integratie met Panopto</span><span class="sxs-lookup"><span data-stu-id="3cca4-103">Tutorial: Azure Active Directory integration with Panopto</span></span>

<span data-ttu-id="3cca4-104">In deze zelfstudie leert u hoe Panopto integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3cca4-104">In this tutorial, you learn how to integrate Panopto with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3cca4-105">Panopto integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="3cca4-105">Integrating Panopto with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3cca4-106">U kunt beheren in Azure AD die toegang tot Panopto heeft</span><span class="sxs-lookup"><span data-stu-id="3cca4-106">You can control in Azure AD who has access to Panopto</span></span>
- <span data-ttu-id="3cca4-107">U kunt uw gebruikers automatisch ophalen aangemeld bij Panopto (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="3cca4-107">You can enable your users to automatically get signed-on to Panopto (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3cca4-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="3cca4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3cca4-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3cca4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3cca4-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3cca4-110">Prerequisites</span></span>

<span data-ttu-id="3cca4-111">Voor het configureren van Azure AD-integratie met Panopto, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="3cca4-111">To configure Azure AD integration with Panopto, you need the following items:</span></span>

- <span data-ttu-id="3cca4-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="3cca4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3cca4-113">Een Panopto eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="3cca4-113">A Panopto single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3cca4-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="3cca4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3cca4-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="3cca4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3cca4-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="3cca4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3cca4-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3cca4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3cca4-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="3cca4-118">Scenario description</span></span>
<span data-ttu-id="3cca4-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="3cca4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3cca4-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="3cca4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3cca4-121">Panopto uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="3cca4-121">Adding Panopto from the gallery</span></span>
2. <span data-ttu-id="3cca4-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3cca4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-panopto-from-the-gallery"></a><span data-ttu-id="3cca4-123">Panopto uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="3cca4-123">Adding Panopto from the gallery</span></span>
<span data-ttu-id="3cca4-124">Voor het configureren van de integratie van Panopto in Azure AD, moet u Panopto uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="3cca4-124">To configure the integration of Panopto into Azure AD, you need to add Panopto from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3cca4-125">**Als u wilt toevoegen Panopto uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3cca4-125">**To add Panopto from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3cca4-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="3cca4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3cca4-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3cca4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3cca4-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3cca4-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="3cca4-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3cca4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="3cca4-133">Typ in het zoekvak **Panopto**.</span><span class="sxs-lookup"><span data-stu-id="3cca4-133">In the search box, type **Panopto**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_search.png)

5. <span data-ttu-id="3cca4-135">Selecteer in het deelvenster resultaten **Panopto**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="3cca4-135">In the results panel, select **Panopto**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3cca4-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3cca4-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="3cca4-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met Panopto op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="3cca4-138">In this section, you configure and test Azure AD single sign-on with Panopto based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3cca4-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Panopto is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3cca4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Panopto is to a user in Azure AD.</span></span> <span data-ttu-id="3cca4-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in Panopto tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="3cca4-140">In other words, a link relationship between an Azure AD user and the related user in Panopto needs to be established.</span></span>

<span data-ttu-id="3cca4-141">Wijs in Panopto, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="3cca4-141">In Panopto, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3cca4-142">Om te configureren en testen van Azure AD eenmalige aanmelding met Panopto, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="3cca4-142">To configure and test Azure AD single sign-on with Panopto, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3cca4-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3cca4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3cca4-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3cca4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3cca4-145">**[Maken van een testgebruiker Panopto](#creating-a-panopto-test-user)**  - Panopto die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="3cca4-145">**[Creating a Panopto test user](#creating-a-panopto-test-user)** - to have a counterpart of Britta Simon in Panopto that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3cca4-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="3cca4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3cca4-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="3cca4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3cca4-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="3cca4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3cca4-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing Panopto configureren.</span><span class="sxs-lookup"><span data-stu-id="3cca4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Panopto application.</span></span>

<span data-ttu-id="3cca4-150">**Voor het configureren van Azure AD eenmalige aanmelding met Panopto, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3cca4-150">**To configure Azure AD single sign-on with Panopto, perform the following steps:**</span></span>

1. <span data-ttu-id="3cca4-151">In de Azure-portal op de **Panopto** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="3cca4-151">In the Azure portal, on the **Panopto** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="3cca4-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="3cca4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_samlbase.png)

3. <span data-ttu-id="3cca4-155">Op de **Panopto domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="3cca4-155">On the **Panopto Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_url.png)

    <span data-ttu-id="3cca4-157">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<tenant-name>.panopto.com`</span><span class="sxs-lookup"><span data-stu-id="3cca4-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.panopto.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3cca4-158">Deze waarde is geen echte.</span><span class="sxs-lookup"><span data-stu-id="3cca4-158">This value is not real.</span></span> <span data-ttu-id="3cca4-159">Deze waarde bijwerken met de werkelijke URL voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="3cca4-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="3cca4-160">Neem contact op met [Panopto Client ondersteuningsteam](mailto:support@panopto.com‎) deze waarde op te halen.</span><span class="sxs-lookup"><span data-stu-id="3cca4-160">Contact [Panopto Client support team](mailto:support@panopto.com‎) to get this value.</span></span> 
 
4. <span data-ttu-id="3cca4-161">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="3cca4-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_certificate.png) 

5. <span data-ttu-id="3cca4-163">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="3cca4-163">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-panopto-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3cca4-165">Op de **Panopto configuratie** sectie, klikt u op **configureren Panopto** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="3cca4-165">On the **Panopto Configuration** section, click **Configure Panopto** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3cca4-166">Kopieer de **SAML entiteit-ID en SAML Single Sign-On Service-URL** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="3cca4-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_configure.png) 

7. <span data-ttu-id="3cca4-168">In een ander browservenster, meld u aan bij uw bedrijf Panopto site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="3cca4-168">In a different web browser window, log in to your Panopto company site as an administrator.</span></span>

8. <span data-ttu-id="3cca4-169">Klik in de werkbalk aan de linkerkant op **System**, en klik vervolgens op **identiteitsproviders**.</span><span class="sxs-lookup"><span data-stu-id="3cca4-169">In the toolbar on the left, click **System**, and then click **Identity Providers**.</span></span>
   
   <span data-ttu-id="3cca4-170">![Systeem](./media/active-directory-saas-panopto-tutorial/ic777670.png "System")</span><span class="sxs-lookup"><span data-stu-id="3cca4-170">![System](./media/active-directory-saas-panopto-tutorial/ic777670.png "System")</span></span>
9. <span data-ttu-id="3cca4-171">Klik op **Provider toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="3cca4-171">Click **Add Provider**.</span></span>
   
   <span data-ttu-id="3cca4-172">![ID-Providers](./media/active-directory-saas-panopto-tutorial/ic777671.png "id-Providers")</span><span class="sxs-lookup"><span data-stu-id="3cca4-172">![Identity Providers](./media/active-directory-saas-panopto-tutorial/ic777671.png "Identity Providers")</span></span>
   
10. <span data-ttu-id="3cca4-173">Voer de volgende stappen uit in de sectie SAML-provider:</span><span class="sxs-lookup"><span data-stu-id="3cca4-173">In the SAML provider section, perform the following steps:</span></span>
   
    <span data-ttu-id="3cca4-174">![SaaS-configuratie](./media/active-directory-saas-panopto-tutorial/ic777672.png "SaaS-configuratie")</span><span class="sxs-lookup"><span data-stu-id="3cca4-174">![SaaS configuration](./media/active-directory-saas-panopto-tutorial/ic777672.png "SaaS configuration")</span></span>
    
    <span data-ttu-id="3cca4-175">a.</span><span class="sxs-lookup"><span data-stu-id="3cca4-175">a.</span></span> <span data-ttu-id="3cca4-176">Van de **providertype** selecteert **SAML20**.</span><span class="sxs-lookup"><span data-stu-id="3cca4-176">From the **Provider Type** list, select **SAML20**.</span></span>    
    
    <span data-ttu-id="3cca4-177">b.</span><span class="sxs-lookup"><span data-stu-id="3cca4-177">b.</span></span> <span data-ttu-id="3cca4-178">In de **exemplaarnaam** textbox, typ een naam voor het exemplaar.</span><span class="sxs-lookup"><span data-stu-id="3cca4-178">In the **Instance Name** textbox, type a name for the instance.</span></span>

    <span data-ttu-id="3cca4-179">c.</span><span class="sxs-lookup"><span data-stu-id="3cca4-179">c.</span></span> <span data-ttu-id="3cca4-180">In de **beschrijving** textbox, typt u een beschrijving.</span><span class="sxs-lookup"><span data-stu-id="3cca4-180">In the **Friendly Description** textbox, type a friendly description.</span></span>
    
    <span data-ttu-id="3cca4-181">d.</span><span class="sxs-lookup"><span data-stu-id="3cca4-181">d.</span></span> <span data-ttu-id="3cca4-182">In **Stuiteren pagina-Url** textbox, plak de waarde van **SAML Single Sign-On Service-URL**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="3cca4-182">In **Bounce Page Url** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3cca4-183">e.</span><span class="sxs-lookup"><span data-stu-id="3cca4-183">e.</span></span> <span data-ttu-id="3cca4-184">In de **verlener** textbox, plak de waarde van **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="3cca4-184">In the **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3cca4-185">f.</span><span class="sxs-lookup"><span data-stu-id="3cca4-185">f.</span></span> <span data-ttu-id="3cca4-186">Open uw base 64-gecodeerde certificaat dat u hebt gedownload vanuit Azure-portal, de inhoud ervan in kopiëren naar het Klembord en plakt u deze naar de **openbare sleutel** textbox.</span><span class="sxs-lookup"><span data-stu-id="3cca4-186">Open your base-64 encoded certificate, which you have downloaded from Azure portal, copy the content of it in to your clipboard, and then paste it to the **Public Key**  textbox.</span></span>

11. <span data-ttu-id="3cca4-187">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="3cca4-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="3cca4-188">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="3cca4-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3cca4-189">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="3cca4-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3cca4-190">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3cca4-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3cca4-191">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="3cca4-191">Creating an Azure AD test user</span></span>

<span data-ttu-id="3cca4-192">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="3cca4-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="3cca4-194">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3cca4-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3cca4-195">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="3cca4-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-panopto-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3cca4-197">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="3cca4-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-panopto-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3cca4-199">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3cca4-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-panopto-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3cca4-201">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="3cca4-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-panopto-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3cca4-203">a.</span><span class="sxs-lookup"><span data-stu-id="3cca4-203">a.</span></span> <span data-ttu-id="3cca4-204">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3cca4-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3cca4-205">b.</span><span class="sxs-lookup"><span data-stu-id="3cca4-205">b.</span></span> <span data-ttu-id="3cca4-206">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3cca4-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3cca4-207">c.</span><span class="sxs-lookup"><span data-stu-id="3cca4-207">c.</span></span> <span data-ttu-id="3cca4-208">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="3cca4-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3cca4-209">d.</span><span class="sxs-lookup"><span data-stu-id="3cca4-209">d.</span></span> <span data-ttu-id="3cca4-210">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="3cca4-210">Click **Create**.</span></span>
 
### <a name="creating-a-panopto-test-user"></a><span data-ttu-id="3cca4-211">Een testgebruiker Panopto maken</span><span class="sxs-lookup"><span data-stu-id="3cca4-211">Creating a Panopto test user</span></span>

<span data-ttu-id="3cca4-212">Er is geen actie-item voor gebruikers inrichten voor Panopto configuratie.</span><span class="sxs-lookup"><span data-stu-id="3cca4-212">There is no action item for you to configure user provisioning to Panopto.</span></span>  
<span data-ttu-id="3cca4-213">Wanneer een toegewezen gebruiker probeert zich aanmelden bij met het toegangsvenster Panopto, Panopto u controleert of de gebruiker bestaat.</span><span class="sxs-lookup"><span data-stu-id="3cca4-213">When an assigned user tries to log in to Panopto using the access panel, Panopto checks whether the user exists.</span></span>  

<span data-ttu-id="3cca4-214">Als er nog geen gebruikersaccount beschikbaar is, wordt het automatisch gemaakt door Panopto.</span><span class="sxs-lookup"><span data-stu-id="3cca4-214">If there is no user account available yet, it is automatically created by Panopto.</span></span>

>[!NOTE]
><span data-ttu-id="3cca4-215">U kunt andere Panopto gebruiker account hulpmiddelen voor het maken of API's die is geleverd door Panopto voor het inrichten van Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="3cca4-215">You can use any other Panopto user account creation tools or APIs provided by Panopto to provision Azure AD user accounts.</span></span>
>
>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3cca4-216">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="3cca4-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3cca4-217">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan Panopto.</span><span class="sxs-lookup"><span data-stu-id="3cca4-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Panopto.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="3cca4-219">**Britta Simon om aan te wijzen Panopto, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="3cca4-219">**To assign Britta Simon to Panopto, perform the following steps:**</span></span>

1. <span data-ttu-id="3cca4-220">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="3cca4-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="3cca4-222">Selecteer in de lijst met toepassingen **Panopto**.</span><span class="sxs-lookup"><span data-stu-id="3cca4-222">In the applications list, select **Panopto**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_app.png) 

3. <span data-ttu-id="3cca4-224">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="3cca4-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="3cca4-226">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="3cca4-226">Click **Add** button.</span></span> <span data-ttu-id="3cca4-227">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3cca4-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="3cca4-229">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="3cca4-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3cca4-230">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3cca4-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3cca4-231">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="3cca4-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3cca4-232">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="3cca4-232">Testing single sign-on</span></span>

<span data-ttu-id="3cca4-233">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="3cca4-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3cca4-234">Als u op de tegel Panopto in het deelvenster toegang, moet u de aanmeldingspagina van Panopto toepassing automatisch ophalen.</span><span class="sxs-lookup"><span data-stu-id="3cca4-234">When you click the Panopto tile in the Access Panel, you should get automatically login page of Panopto application.</span></span>
<span data-ttu-id="3cca4-235">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3cca4-235">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3cca4-236">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="3cca4-236">Additional resources</span></span>

* [<span data-ttu-id="3cca4-237">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3cca4-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3cca4-238">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3cca4-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_203.png

