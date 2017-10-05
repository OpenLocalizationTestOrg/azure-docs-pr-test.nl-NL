---
title: 'Zelfstudie: Azure Active Directory-integratie met ADP eTime | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en ADP eTime.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a3e9f0be-19ed-4b99-a180-619e7624fc26
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 31fed307a32e629d00aab7cc9d5167ee16d83936
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-etime"></a><span data-ttu-id="b9d43-103">Zelfstudie: Azure Active Directory-integratie met ADP eTime</span><span class="sxs-lookup"><span data-stu-id="b9d43-103">Tutorial: Azure Active Directory integration with ADP eTime</span></span>

<span data-ttu-id="b9d43-104">In deze zelfstudie leert u hoe ADP eTime integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b9d43-104">In this tutorial, you learn how to integrate ADP eTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b9d43-105">ADP eTime integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="b9d43-105">Integrating ADP eTime with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b9d43-106">U kunt beheren in Azure AD die toegang tot ADP eTime heeft</span><span class="sxs-lookup"><span data-stu-id="b9d43-106">You can control in Azure AD who has access to ADP eTime</span></span>
- <span data-ttu-id="b9d43-107">U kunt uw gebruikers automatisch ophalen aangemeld bij ADP eTime (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="b9d43-107">You can enable your users to automatically get signed-on to ADP eTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b9d43-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="b9d43-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b9d43-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b9d43-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9d43-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b9d43-110">Prerequisites</span></span>

<span data-ttu-id="b9d43-111">Voor het configureren van Azure AD-integratie met ADP eTime, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="b9d43-111">To configure Azure AD integration with ADP eTime, you need the following items:</span></span>

- <span data-ttu-id="b9d43-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="b9d43-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b9d43-113">Een ADP eTime eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="b9d43-113">An ADP eTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b9d43-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="b9d43-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b9d43-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="b9d43-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b9d43-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="b9d43-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b9d43-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b9d43-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b9d43-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="b9d43-118">Scenario description</span></span>
<span data-ttu-id="b9d43-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="b9d43-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b9d43-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="b9d43-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b9d43-121">ADP eTime uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="b9d43-121">Adding ADP eTime from the gallery</span></span>
2. <span data-ttu-id="b9d43-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b9d43-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-etime-from-the-gallery"></a><span data-ttu-id="b9d43-123">ADP eTime uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="b9d43-123">Adding ADP eTime from the gallery</span></span>
<span data-ttu-id="b9d43-124">Voor het configureren van de integratie van ADP eTime in Azure AD, moet u ADP eTime uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="b9d43-124">To configure the integration of ADP eTime into Azure AD, you need to add ADP eTime from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b9d43-125">**Als u wilt toevoegen ADP eTime uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b9d43-125">**To add ADP eTime from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b9d43-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b9d43-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b9d43-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b9d43-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b9d43-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b9d43-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="b9d43-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b9d43-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="b9d43-133">Typ in het zoekvak **ADP eTime**.</span><span class="sxs-lookup"><span data-stu-id="b9d43-133">In the search box, type **ADP eTime**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_search.png)

5. <span data-ttu-id="b9d43-135">Selecteer in het deelvenster resultaten **ADP eTime**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="b9d43-135">In the results panel, select **ADP eTime**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b9d43-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b9d43-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b9d43-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met ADP eTime op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="b9d43-138">In this section, you configure and test Azure AD single sign-on with ADP eTime based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b9d43-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in ADP eTime is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9d43-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ADP eTime is to a user in Azure AD.</span></span> <span data-ttu-id="b9d43-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in ADP eTime tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="b9d43-140">In other words, a link relationship between an Azure AD user and the related user in ADP eTime needs to be established.</span></span>

<span data-ttu-id="b9d43-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="b9d43-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ADP eTime.</span></span>

<span data-ttu-id="b9d43-142">Om te configureren en testen van Azure AD eenmalige aanmelding met ADP eTime, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="b9d43-142">To configure and test Azure AD single sign-on with ADP eTime, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b9d43-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b9d43-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b9d43-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b9d43-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b9d43-145">**[Maken van een gebruiker ADP eTime test](#creating-an-adp-etime-test-user)**  - hebben een equivalent van Britta Simon in ADP eTime die is gekoppeld aan de Azure AD-weergave van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b9d43-145">**[Creating an ADP eTime test user](#creating-an-adp-etime-test-user)** - to have a counterpart of Britta Simon in ADP eTime that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b9d43-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b9d43-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b9d43-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="b9d43-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b9d43-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="b9d43-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b9d43-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw ADP eTime-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b9d43-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ADP eTime application.</span></span>

<span data-ttu-id="b9d43-150">**Voor het configureren van Azure AD eenmalige aanmelding met ADP eTime, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b9d43-150">**To configure Azure AD single sign-on with ADP eTime, perform the following steps:**</span></span>

1. <span data-ttu-id="b9d43-151">In de Azure-portal op de **ADP eTime** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="b9d43-151">In the Azure portal, on the **ADP eTime** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="b9d43-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="b9d43-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_samlbase.png)

3. <span data-ttu-id="b9d43-155">Op de **ADP eTime domein en URL's** sectie, voert u de volgende stap:</span><span class="sxs-lookup"><span data-stu-id="b9d43-155">On the **ADP eTime Domain and URLs** section, perform the following step:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_url.png)

    <span data-ttu-id="b9d43-157">a.</span><span class="sxs-lookup"><span data-stu-id="b9d43-157">a.</span></span> <span data-ttu-id="b9d43-158">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<servername>.adp.com`</span><span class="sxs-lookup"><span data-stu-id="b9d43-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<servername>.adp.com`</span></span>

    <span data-ttu-id="b9d43-159">b.</span><span class="sxs-lookup"><span data-stu-id="b9d43-159">b.</span></span> <span data-ttu-id="b9d43-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span><span class="sxs-lookup"><span data-stu-id="b9d43-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span></span> 
 
    > [!NOTE] 
    > <span data-ttu-id="b9d43-161">Deze waarden zijn niet de werkelijke.</span><span class="sxs-lookup"><span data-stu-id="b9d43-161">These values are not the real.</span></span> <span data-ttu-id="b9d43-162">Deze waarden bijwerken met het werkelijke antwoord-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="b9d43-162">Update these values with the actual Reply URL and Identifier.</span></span> <span data-ttu-id="b9d43-163">Neem contact op met [ADP eTime ondersteuningsteam](https://www.adp.com/contact-us/overview.aspx) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="b9d43-163">Contact [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) to get these values.</span></span>

4. <span data-ttu-id="b9d43-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het XML-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="b9d43-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_certificate.png) 

5. <span data-ttu-id="b9d43-166">De toepassing van de eTime ADP verwacht de SAML-asserties in een specifieke indeling waarvoor u aangepaste kenmerktoewijzingen toevoegen aan uw configuratie van SAML-token kenmerken.</span><span class="sxs-lookup"><span data-stu-id="b9d43-166">The ADP eTime application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="b9d43-167">De volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="b9d43-167">The following screenshot shows an example for this.</span></span> <span data-ttu-id="b9d43-168">De naam van de claim wordt altijd worden **'PersonImmutableID'** en de waarde die we hebben toegewezen aan ExtensionAttribute2 waarin de werknemer-id van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b9d43-168">The claim name will always be **"PersonImmutableID"** and the value of which we have mapped to ExtensionAttribute2 which contains the EmployeeID of the user.</span></span> 

    <span data-ttu-id="b9d43-169">Hier wordt de gebruiker toewijzen van Azure AD aan ADP eTime worden uitgevoerd op de werknemer-id maar u kunt dit toewijzen aan een andere waarde ook op basis van de toepassingsinstellingen van uw.</span><span class="sxs-lookup"><span data-stu-id="b9d43-169">Here the user mapping from Azure AD to ADP eTime will be done on the EmployeeID but you can map this to a different value also based on your application settings.</span></span> <span data-ttu-id="b9d43-170">Dus neem werk met [ADP eTime ondersteuningsteam](https://www.adp.com/contact-us/overview.aspx) eerst voor het gebruik van de juiste id van een gebruiker en wijs die waarde met de **'PersonImmutableID'** claim.</span><span class="sxs-lookup"><span data-stu-id="b9d43-170">So please work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) first to use the correct identifier of a user and map that value with the **"PersonImmutableID"** claim.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_attribute.png)

6. <span data-ttu-id="b9d43-172">In de **gebruikerskenmerken** sectie op de **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in de afbeelding en de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="b9d43-172">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="b9d43-173">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="b9d43-173">Attribute Name</span></span> | <span data-ttu-id="b9d43-174">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="b9d43-174">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="b9d43-175">PersonImmutableID</span><span class="sxs-lookup"><span data-stu-id="b9d43-175">PersonImmutableID</span></span> | <span data-ttu-id="b9d43-176">User.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="b9d43-176">user.extensionattribute2</span></span> |
    
    <span data-ttu-id="b9d43-177">a.</span><span class="sxs-lookup"><span data-stu-id="b9d43-177">a.</span></span> <span data-ttu-id="b9d43-178">Klik op **toevoegen kenmerk** openen de **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b9d43-178">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="b9d43-181">b.</span><span class="sxs-lookup"><span data-stu-id="b9d43-181">b.</span></span> <span data-ttu-id="b9d43-182">In de **naam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="b9d43-182">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="b9d43-183">c.</span><span class="sxs-lookup"><span data-stu-id="b9d43-183">c.</span></span> <span data-ttu-id="b9d43-184">Van de **waarde** typt u de waarde van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="b9d43-184">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="b9d43-185">d.</span><span class="sxs-lookup"><span data-stu-id="b9d43-185">d.</span></span> <span data-ttu-id="b9d43-186">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b9d43-186">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b9d43-187">Voordat u de SAML-bevestiging configureren kunt, moet u contact op met uw [ADP eTime ondersteuningsteam](https://www.adp.com/contact-us/overview.aspx) en vraagt u de waarde van het kenmerk unieke id voor uw tenant.</span><span class="sxs-lookup"><span data-stu-id="b9d43-187">Before you can configure the SAML assertion, you need to contact your [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="b9d43-188">U moet deze waarde voor het configureren van de aangepaste claim voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="b9d43-188">You need this value to configure the custom claim for your application.</span></span> 

7. <span data-ttu-id="b9d43-189">Op de **ADP eTime configuratie** sectie, klikt u op **ADP configureren eTime** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="b9d43-189">On the **ADP eTime Configuration** section, click **Configure ADP eTime** to open **Configure sign-on** window.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_configure.png) 

8. <span data-ttu-id="b9d43-191">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="b9d43-191">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adpetime-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="b9d43-193">Eenmalige aanmelding configureren op **ADP eTime** zijde, moet u de gedownloade verzenden **Metadata XML** naar [ADP eTime ondersteuningsteam](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="b9d43-193">To configure single sign-on on **ADP eTime** side, you need to send the downloaded **Metadata XML** to [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx).</span></span> 

> [!TIP]
> <span data-ttu-id="b9d43-194">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="b9d43-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b9d43-195">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="b9d43-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b9d43-196">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b9d43-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b9d43-197">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="b9d43-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="b9d43-198">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b9d43-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="b9d43-200">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b9d43-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b9d43-201">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="b9d43-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adpetime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b9d43-203">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="b9d43-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adpetime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b9d43-205">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b9d43-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adpetime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b9d43-207">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="b9d43-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-adpetime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b9d43-209">a.</span><span class="sxs-lookup"><span data-stu-id="b9d43-209">a.</span></span> <span data-ttu-id="b9d43-210">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b9d43-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b9d43-211">b.</span><span class="sxs-lookup"><span data-stu-id="b9d43-211">b.</span></span> <span data-ttu-id="b9d43-212">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b9d43-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b9d43-213">c.</span><span class="sxs-lookup"><span data-stu-id="b9d43-213">c.</span></span> <span data-ttu-id="b9d43-214">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="b9d43-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b9d43-215">d.</span><span class="sxs-lookup"><span data-stu-id="b9d43-215">d.</span></span> <span data-ttu-id="b9d43-216">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="b9d43-216">Click **Create**.</span></span>
 
### <a name="creating-an-adp-etime-test-user"></a><span data-ttu-id="b9d43-217">Maken van een gebruiker ADP eTime testen</span><span class="sxs-lookup"><span data-stu-id="b9d43-217">Creating an ADP eTime test user</span></span>

<span data-ttu-id="b9d43-218">Het doel van deze sectie is het maken van een gebruiker Britta Simon in ADP eTime genoemd.</span><span class="sxs-lookup"><span data-stu-id="b9d43-218">The objective of this section is to create a user called Britta Simon in ADP eTime.</span></span> <span data-ttu-id="b9d43-219">Werken met [ADP eTime ondersteuningsteam](https://www.adp.com/contact-us/overview.aspx) de gebruikers in het ADP eTime account toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b9d43-219">Work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) to add the users in the ADP eTime account.</span></span> 
   
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b9d43-220">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9d43-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b9d43-221">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door het verlenen van toegang tot ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="b9d43-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ADP eTime.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="b9d43-223">**Britta Simon om aan te wijzen ADP eTime, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="b9d43-223">**To assign Britta Simon to ADP eTime, perform the following steps:**</span></span>

1. <span data-ttu-id="b9d43-224">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="b9d43-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="b9d43-226">Selecteer in de lijst met toepassingen **ADP eTime**.</span><span class="sxs-lookup"><span data-stu-id="b9d43-226">In the applications list, select **ADP eTime**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_app.png) 

3. <span data-ttu-id="b9d43-228">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="b9d43-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="b9d43-230">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="b9d43-230">Click **Add** button.</span></span> <span data-ttu-id="b9d43-231">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b9d43-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="b9d43-233">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="b9d43-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b9d43-234">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b9d43-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b9d43-235">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b9d43-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b9d43-236">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="b9d43-236">Testing single sign-on</span></span>

<span data-ttu-id="b9d43-237">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="b9d43-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b9d43-238">Als u op de tegel ADP eTime in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw ADP eTime-toepassing.</span><span class="sxs-lookup"><span data-stu-id="b9d43-238">When you click the ADP eTime tile in the Access Panel, you should get automatically signed-on to your ADP eTime application.</span></span>
<span data-ttu-id="b9d43-239">Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b9d43-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b9d43-240">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="b9d43-240">Additional resources</span></span>

* [<span data-ttu-id="b9d43-241">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b9d43-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b9d43-242">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b9d43-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_203.png

