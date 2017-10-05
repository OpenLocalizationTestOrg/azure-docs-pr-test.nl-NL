---
title: 'Zelfstudie: Azure Active Directory-integratie met DigiCert | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en DigiCert.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 646f3129-aa67-4875-9073-1d0b6a3173d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 2ceb3c0833edcd4ecd875c5e8006961ed7216c66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-digicert"></a><span data-ttu-id="103db-103">Zelfstudie: Azure Active Directory-integratie met DigiCert</span><span class="sxs-lookup"><span data-stu-id="103db-103">Tutorial: Azure Active Directory integration with DigiCert</span></span>

<span data-ttu-id="103db-104">In deze zelfstudie leert u hoe DigiCert integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="103db-104">In this tutorial, you learn how to integrate DigiCert with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="103db-105">DigiCert integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="103db-105">Integrating DigiCert with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="103db-106">U kunt beheren in Azure AD die toegang tot DigiCert heeft</span><span class="sxs-lookup"><span data-stu-id="103db-106">You can control in Azure AD who has access to DigiCert</span></span>
- <span data-ttu-id="103db-107">U kunt uw gebruikers automatisch ophalen aangemeld bij DigiCert (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="103db-107">You can enable your users to automatically get signed-on to DigiCert (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="103db-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="103db-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="103db-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="103db-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="103db-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="103db-110">Prerequisites</span></span>

<span data-ttu-id="103db-111">Voor het configureren van Azure AD-integratie met DigiCert, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="103db-111">To configure Azure AD integration with DigiCert, you need the following items:</span></span>

- <span data-ttu-id="103db-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="103db-112">An Azure AD subscription</span></span>
- <span data-ttu-id="103db-113">Een DigiCert eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="103db-113">A DigiCert single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="103db-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="103db-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="103db-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="103db-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="103db-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="103db-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="103db-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="103db-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="103db-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="103db-118">Scenario description</span></span>
<span data-ttu-id="103db-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="103db-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="103db-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="103db-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="103db-121">DigiCert uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="103db-121">Adding DigiCert from the gallery</span></span>
2. <span data-ttu-id="103db-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="103db-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-digicert-from-the-gallery"></a><span data-ttu-id="103db-123">DigiCert uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="103db-123">Adding DigiCert from the gallery</span></span>
<span data-ttu-id="103db-124">Voor het configureren van de integratie van DigiCert in Azure AD, moet u DigiCert uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="103db-124">To configure the integration of DigiCert into Azure AD, you need to add DigiCert from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="103db-125">**Als u wilt toevoegen DigiCert uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="103db-125">**To add DigiCert from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="103db-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="103db-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="103db-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="103db-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="103db-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="103db-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="103db-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="103db-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="103db-133">Typ in het zoekvak **DigiCert**.</span><span class="sxs-lookup"><span data-stu-id="103db-133">In the search box, type **DigiCert**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_search.png)

5. <span data-ttu-id="103db-135">Selecteer in het deelvenster resultaten **DigiCert**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="103db-135">In the results panel, select **DigiCert**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="103db-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="103db-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="103db-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met DigiCert op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="103db-138">In this section, you configure and test Azure AD single sign-on with DigiCert based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="103db-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in DigiCert is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="103db-139">For single sign-on to work, Azure AD needs to know what the counterpart user in DigiCert is to a user in Azure AD.</span></span> <span data-ttu-id="103db-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante DigiCert-gebruiker worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="103db-140">In other words, a link relationship between an Azure AD user and the related user in DigiCert needs to be established.</span></span>

<span data-ttu-id="103db-141">Wijs in DigiCert, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="103db-141">In DigiCert, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="103db-142">Om te configureren en testen van Azure AD eenmalige aanmelding met DigiCert, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="103db-142">To configure and test Azure AD single sign-on with DigiCert, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="103db-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="103db-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="103db-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="103db-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="103db-145">**[Maken van een testgebruiker DigiCert](#creating-a-digicert-test-user)**  - DigiCert die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="103db-145">**[Creating a DigiCert test user](#creating-a-digicert-test-user)** - to have a counterpart of Britta Simon in DigiCert that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="103db-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="103db-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="103db-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="103db-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="103db-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="103db-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="103db-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing DigiCert configureren.</span><span class="sxs-lookup"><span data-stu-id="103db-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your DigiCert application.</span></span>

<span data-ttu-id="103db-150">**Voor het configureren van Azure AD eenmalige aanmelding met DigiCert, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="103db-150">**To configure Azure AD single sign-on with DigiCert, perform the following steps:**</span></span>

1. <span data-ttu-id="103db-151">In de Azure-portal op de **DigiCert** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="103db-151">In the Azure portal, on the **DigiCert** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="103db-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="103db-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_samlbase.png)

3. <span data-ttu-id="103db-155">Op de **DigiCert-domein en de URL's** sectie, de gebruiker heeft geen alle stappen uitvoeren als de app al vooraf is geïntegreerd met Azure.</span><span class="sxs-lookup"><span data-stu-id="103db-155">On the **DigiCert Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_url.png)

4. <span data-ttu-id="103db-157">De SAML-asserties verwacht DigiCert toepassing in een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="103db-157">DigiCert application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="103db-158">Configureer de volgende claims voor deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="103db-158">Configure the following claims for this application.</span></span> <span data-ttu-id="103db-159">U kunt beheren de waarden van deze kenmerken van de '**gebruikerskenmerken**' sectie op de pagina van de toepassing-integratie.</span><span class="sxs-lookup"><span data-stu-id="103db-159">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="103db-160">De volgende Schermafbeelding toont een voorbeeld voor deze configuratie.</span><span class="sxs-lookup"><span data-stu-id="103db-160">The following screenshot shows an example for this configuration.</span></span> 

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_attributes.png)
    
5. <span data-ttu-id="103db-162">In de **gebruikerskenmerken** sectie op de **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in de afbeelding en de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="103db-162">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="103db-163">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="103db-163">Attribute Name</span></span> | <span data-ttu-id="103db-164">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="103db-164">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="103db-165">Bedrijf</span><span class="sxs-lookup"><span data-stu-id="103db-165">company</span></span> | <span data-ttu-id="103db-166">< companycode ></span><span class="sxs-lookup"><span data-stu-id="103db-166">< companycode ></span></span> |
    | <span data-ttu-id="103db-167">digicertrole</span><span class="sxs-lookup"><span data-stu-id="103db-167">digicertrole</span></span> | <span data-ttu-id="103db-168">CanAccessCertCentral</span><span class="sxs-lookup"><span data-stu-id="103db-168">CanAccessCertCentral</span></span> |

    > [!Note]
    > <span data-ttu-id="103db-169">De waarde van **bedrijf** kenmerk is niet echt.</span><span class="sxs-lookup"><span data-stu-id="103db-169">The value of **company** attribute is not real.</span></span> <span data-ttu-id="103db-170">Deze waarde bijwerken met de werkelijke bedrijfscode.</span><span class="sxs-lookup"><span data-stu-id="103db-170">Update this value with actual company code.</span></span> <span data-ttu-id="103db-171">Om de waarde van **bedrijf** Neem contact op met het kenmerk [DigiCert ondersteuningsteam](mailto:support@digicert.com).</span><span class="sxs-lookup"><span data-stu-id="103db-171">To get the value of **company** attribute contact [DigiCert support team](mailto:support@digicert.com).</span></span>

    <span data-ttu-id="103db-172">a.</span><span class="sxs-lookup"><span data-stu-id="103db-172">a.</span></span> <span data-ttu-id="103db-173">Klik op **toevoegen kenmerk** openen de **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="103db-173">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-digicert-tutorial/tutorial_attribute_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-digicert-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="103db-176">b.</span><span class="sxs-lookup"><span data-stu-id="103db-176">b.</span></span> <span data-ttu-id="103db-177">In de **naam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="103db-177">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="103db-178">c.</span><span class="sxs-lookup"><span data-stu-id="103db-178">c.</span></span> <span data-ttu-id="103db-179">Van de **waarde** typt u de waarde van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="103db-179">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="103db-180">d.</span><span class="sxs-lookup"><span data-stu-id="103db-180">d.</span></span> <span data-ttu-id="103db-181">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="103db-181">Click **Ok**.</span></span> 

6. <span data-ttu-id="103db-182">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.</span><span class="sxs-lookup"><span data-stu-id="103db-182">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_certificate.png) 

7. <span data-ttu-id="103db-184">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="103db-184">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-digicert-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="103db-186">Eenmalige aanmelding configureren op **DigiCert** zijde, moet u de gedownloade verzenden **Metadata XML** naar [DigiCert ondersteuningsteam](mailto:support@digicert.com).</span><span class="sxs-lookup"><span data-stu-id="103db-186">To configure single sign-on on **DigiCert** side, you need to send the downloaded **Metadata XML** to [DigiCert support team](mailto:support@digicert.com).</span></span> <span data-ttu-id="103db-187">Ze deze instelling zodat de SAML SSO-verbinding juist is ingesteld op beide zijden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="103db-187">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="103db-188">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="103db-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="103db-189">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="103db-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="103db-190">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="103db-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="103db-191">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="103db-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="103db-192">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="103db-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="103db-194">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="103db-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="103db-195">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="103db-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-digicert-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="103db-197">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="103db-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-digicert-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="103db-199">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="103db-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-digicert-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="103db-201">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="103db-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-digicert-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="103db-203">a.</span><span class="sxs-lookup"><span data-stu-id="103db-203">a.</span></span> <span data-ttu-id="103db-204">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="103db-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="103db-205">b.</span><span class="sxs-lookup"><span data-stu-id="103db-205">b.</span></span> <span data-ttu-id="103db-206">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="103db-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="103db-207">c.</span><span class="sxs-lookup"><span data-stu-id="103db-207">c.</span></span> <span data-ttu-id="103db-208">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="103db-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="103db-209">d.</span><span class="sxs-lookup"><span data-stu-id="103db-209">d.</span></span> <span data-ttu-id="103db-210">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="103db-210">Click **Create**.</span></span>
 
### <a name="creating-a-digicert-test-user"></a><span data-ttu-id="103db-211">Een testgebruiker DigiCert maken</span><span class="sxs-lookup"><span data-stu-id="103db-211">Creating a DigiCert test user</span></span>

<span data-ttu-id="103db-212">In deze sectie kunt u een gebruiker Britta Simon aangeroepen in DigiCert maken.</span><span class="sxs-lookup"><span data-stu-id="103db-212">In this section, you create a user called Britta Simon in DigiCert.</span></span> <span data-ttu-id="103db-213">Neem contact op met [DigiCert ondersteuningsteam](mailto:support@digicert.com) toevoegen van de gebruikers in DigiCert.</span><span class="sxs-lookup"><span data-stu-id="103db-213">Please work with [DigiCert support team](mailto:support@digicert.com) to add the users in DigiCert.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="103db-214">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="103db-214">Assigning the Azure AD test user</span></span>

<span data-ttu-id="103db-215">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan DigiCert.</span><span class="sxs-lookup"><span data-stu-id="103db-215">In this section, you enable Britta Simon to use Azure single sign-on by granting access to DigiCert.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="103db-217">**Britta Simon om aan te wijzen DigiCert, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="103db-217">**To assign Britta Simon to DigiCert, perform the following steps:**</span></span>

1. <span data-ttu-id="103db-218">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="103db-218">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="103db-220">Selecteer in de lijst met toepassingen **DigiCert**.</span><span class="sxs-lookup"><span data-stu-id="103db-220">In the applications list, select **DigiCert**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_app.png) 

3. <span data-ttu-id="103db-222">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="103db-222">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="103db-224">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="103db-224">Click **Add** button.</span></span> <span data-ttu-id="103db-225">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="103db-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="103db-227">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="103db-227">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="103db-228">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="103db-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="103db-229">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="103db-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="103db-230">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="103db-230">Testing single sign-on</span></span>

<span data-ttu-id="103db-231">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="103db-231">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="103db-232">Als u op de tegel DigiCert in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing DeigiCert.</span><span class="sxs-lookup"><span data-stu-id="103db-232">When you click the DigiCert tile in the Access Panel, you should get automatically signed-on to your DeigiCert application.</span></span>
<span data-ttu-id="103db-233">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="103db-233">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="103db-234">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="103db-234">Additional resources</span></span>

* [<span data-ttu-id="103db-235">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="103db-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="103db-236">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="103db-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_203.png

