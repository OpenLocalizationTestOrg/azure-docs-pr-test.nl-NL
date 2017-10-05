---
title: 'Zelfstudie: Azure Active Directory-integratie met AppDynamics | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en AppDynamics.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 25fd1df0-411c-4f55-8be3-4273b543100f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 634e68bdb937eba68b27b824dc62fe2677e24ffe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-appdynamics"></a><span data-ttu-id="50233-103">Zelfstudie: Azure Active Directory-integratie met AppDynamics</span><span class="sxs-lookup"><span data-stu-id="50233-103">Tutorial: Azure Active Directory integration with AppDynamics</span></span>

<span data-ttu-id="50233-104">In deze zelfstudie leert u hoe AppDynamics integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="50233-104">In this tutorial, you learn how to integrate AppDynamics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="50233-105">AppDynamics integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="50233-105">Integrating AppDynamics with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="50233-106">U kunt beheren in Azure AD die toegang tot AppDynamics heeft</span><span class="sxs-lookup"><span data-stu-id="50233-106">You can control in Azure AD who has access to AppDynamics</span></span>
- <span data-ttu-id="50233-107">U kunt uw gebruikers automatisch ophalen aangemeld bij AppDynamics (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="50233-107">You can enable your users to automatically get signed-on to AppDynamics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="50233-108">U kunt uw accounts op één centrale locatie - en de Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="50233-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="50233-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="50233-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="50233-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="50233-110">Prerequisites</span></span>

<span data-ttu-id="50233-111">Voor het configureren van Azure AD-integratie met AppDynamics, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="50233-111">To configure Azure AD integration with AppDynamics, you need the following items:</span></span>

- <span data-ttu-id="50233-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="50233-112">An Azure AD subscription</span></span>
- <span data-ttu-id="50233-113">Een AppDynamics eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="50233-113">An AppDynamics single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="50233-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="50233-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="50233-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="50233-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="50233-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="50233-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="50233-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="50233-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="50233-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="50233-118">Scenario description</span></span>
<span data-ttu-id="50233-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="50233-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="50233-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="50233-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="50233-121">AppDynamics uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="50233-121">Adding AppDynamics from the gallery</span></span>
2. <span data-ttu-id="50233-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="50233-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-appdynamics-from-the-gallery"></a><span data-ttu-id="50233-123">AppDynamics uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="50233-123">Adding AppDynamics from the gallery</span></span>
<span data-ttu-id="50233-124">Voor het configureren van de integratie van AppDynamics in Azure AD, moet u AppDynamics uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="50233-124">To configure the integration of AppDynamics into Azure AD, you need to add AppDynamics from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="50233-125">**Als u wilt toevoegen AppDynamics uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="50233-125">**To add AppDynamics from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="50233-126">In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="50233-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="50233-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="50233-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="50233-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="50233-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="50233-131">Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="50233-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="50233-133">Typ in het zoekvak **AppDynamics**.</span><span class="sxs-lookup"><span data-stu-id="50233-133">In the search box, type **AppDynamics**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_search.png)

5. <span data-ttu-id="50233-135">Selecteer in het deelvenster resultaten **AppDynamics**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="50233-135">In the results panel, select **AppDynamics**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="50233-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="50233-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="50233-138">In deze sectie kunt u configureren en testen eenmalige aanmelding Azure AD met AppDynamics op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="50233-138">In this section, you configure and test Azure AD single sign-on with AppDynamics based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="50233-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in AppDynamics is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="50233-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AppDynamics is to a user in Azure AD.</span></span> <span data-ttu-id="50233-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in AppDynamics tot stand worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="50233-140">In other words, a link relationship between an Azure AD user and the related user in AppDynamics needs to be established.</span></span>

<span data-ttu-id="50233-141">Wijs in AppDynamics, de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="50233-141">In AppDynamics, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="50233-142">Om te configureren en testen van Azure AD eenmalige aanmelding met AppDynamics, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="50233-142">To configure and test Azure AD single sign-on with AppDynamics, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="50233-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="50233-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="50233-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="50233-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="50233-145">**[Maken van een testgebruiker AppDynamics](#creating-an-appdynamics-test-user)**  - AppDynamics die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.</span><span class="sxs-lookup"><span data-stu-id="50233-145">**[Creating an AppDynamics test user](#creating-an-appdynamics-test-user)** - to have a counterpart of Britta Simon in AppDynamics that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="50233-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="50233-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="50233-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="50233-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="50233-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="50233-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="50233-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding in uw toepassing AppDynamics configureren.</span><span class="sxs-lookup"><span data-stu-id="50233-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AppDynamics application.</span></span>

<span data-ttu-id="50233-150">**Voor het configureren van Azure AD eenmalige aanmelding met AppDynamics, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="50233-150">**To configure Azure AD single sign-on with AppDynamics, perform the following steps:**</span></span>

1. <span data-ttu-id="50233-151">In de Azure-portal op de **AppDynamics** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="50233-151">In the Azure portal, on the **AppDynamics** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="50233-153">Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="50233-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_samlbase.png)

3. <span data-ttu-id="50233-155">Op de **AppDynamics domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="50233-155">On the **AppDynamics Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_url.png)

    <span data-ttu-id="50233-157">a.</span><span class="sxs-lookup"><span data-stu-id="50233-157">a.</span></span> <span data-ttu-id="50233-158">In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.saas.appdynamics.com`</span><span class="sxs-lookup"><span data-stu-id="50233-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.saas.appdynamics.com`</span></span>

    <span data-ttu-id="50233-159">b.</span><span class="sxs-lookup"><span data-stu-id="50233-159">b.</span></span> <span data-ttu-id="50233-160">In de **id** textbox, typ een URL met het volgende patroon volgen:`https://<companyname>.saas.appdynamics.com/controller`</span><span class="sxs-lookup"><span data-stu-id="50233-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.saas.appdynamics.com/controller`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="50233-161">Deze waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="50233-161">These values are not real.</span></span> <span data-ttu-id="50233-162">Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id.</span><span class="sxs-lookup"><span data-stu-id="50233-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="50233-163">Neem contact op met [AppDynamics Client ondersteuningsteam](https://www.appdynamics.com/support/) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="50233-163">Contact [AppDynamics Client support team](https://www.appdynamics.com/support/) to get these values.</span></span> 
 
4. <span data-ttu-id="50233-164">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="50233-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_certificate.png) 

5. <span data-ttu-id="50233-166">Klik op **opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="50233-166">Click **Save** button.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-appdynamics-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="50233-168">Op de **AppDynamics configuratie** sectie, klikt u op **configureren AppDynamics** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="50233-168">On the **AppDynamics Configuration** section, click **Configure AppDynamics** to open **Configure sign-on** window.</span></span> <span data-ttu-id="50233-169">Kopieer de **Sign-Out URL's, en SAML Single Sign-On Service** van de **Naslaggids punt.**</span><span class="sxs-lookup"><span data-stu-id="50233-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_configure.png) 

7. <span data-ttu-id="50233-171">In een ander browservenster, meld u aan bij uw bedrijf AppDynamics site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="50233-171">In a different web browser window, log in to your AppDynamics company site as an administrator.</span></span>

8. <span data-ttu-id="50233-172">Klik in de werkbalk bovenaan op **instellingen**, en klik vervolgens op **beheer**.</span><span class="sxs-lookup"><span data-stu-id="50233-172">In the toolbar on the top, click **Settings**, and then click **Administration**.</span></span>
   
    <span data-ttu-id="50233-173">![Beheer](./media/active-directory-saas-appdynamics-tutorial/ic790216.png "beheer")</span><span class="sxs-lookup"><span data-stu-id="50233-173">![Administration](./media/active-directory-saas-appdynamics-tutorial/ic790216.png "Administration")</span></span>

9. <span data-ttu-id="50233-174">Klik op de **verificatieprovider** tabblad.</span><span class="sxs-lookup"><span data-stu-id="50233-174">Click the **Authentication Provider** tab.</span></span>
   
    <span data-ttu-id="50233-175">![Verificatieprovider](./media/active-directory-saas-appdynamics-tutorial/ic790224.png "verificatieprovider")</span><span class="sxs-lookup"><span data-stu-id="50233-175">![Authentication Provider](./media/active-directory-saas-appdynamics-tutorial/ic790224.png "Authentication Provider")</span></span>

10. <span data-ttu-id="50233-176">In de **verificatieprovider** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="50233-176">In the **Authentication Provider** section, perform the following steps:</span></span>
   
    <span data-ttu-id="50233-177">![De SAML-configuratie](./media/active-directory-saas-appdynamics-tutorial/ic790225.png "SAML-configuratie")</span><span class="sxs-lookup"><span data-stu-id="50233-177">![SAML Configuration](./media/active-directory-saas-appdynamics-tutorial/ic790225.png "SAML Configuration")</span></span>   

    <span data-ttu-id="50233-178">a.</span><span class="sxs-lookup"><span data-stu-id="50233-178">a.</span></span> <span data-ttu-id="50233-179">Als **verificatieprovider**, selecteer **SAML**.</span><span class="sxs-lookup"><span data-stu-id="50233-179">As **Authentication Provider**, select **SAML**.</span></span>

    <span data-ttu-id="50233-180">b.</span><span class="sxs-lookup"><span data-stu-id="50233-180">b.</span></span> <span data-ttu-id="50233-181">In de **aanmeldings-URL** textbox, plak de waarde van **SAML Single Sign-On Service-URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="50233-181">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="50233-182">c.</span><span class="sxs-lookup"><span data-stu-id="50233-182">c.</span></span> <span data-ttu-id="50233-183">In de **afmelding URL** textbox, plak de waarde van **Sign-Out URL** die u hebt gekopieerd vanuit Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="50233-183">In the **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="50233-184">d.</span><span class="sxs-lookup"><span data-stu-id="50233-184">d.</span></span> <span data-ttu-id="50233-185">Open uw base-64 gecodeerde certificaat in Kladblok, Kopieer de inhoud ervan naar het Klembord en plakt u deze naar de **certificaat** tekstvak</span><span class="sxs-lookup"><span data-stu-id="50233-185">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** textbox</span></span>

    <span data-ttu-id="50233-186">e.</span><span class="sxs-lookup"><span data-stu-id="50233-186">e.</span></span> <span data-ttu-id="50233-187">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="50233-187">Click **Save**.</span></span>

     <span data-ttu-id="50233-188">![Sla](./media/active-directory-saas-appdynamics-tutorial/ic777673.png "opslaan")</span><span class="sxs-lookup"><span data-stu-id="50233-188">![Save](./media/active-directory-saas-appdynamics-tutorial/ic777673.png "Save")</span></span>

> [!TIP]
> <span data-ttu-id="50233-189">U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!</span><span class="sxs-lookup"><span data-stu-id="50233-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="50233-190">Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="50233-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="50233-191">U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="50233-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="50233-192">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="50233-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="50233-193">Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="50233-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="50233-195">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="50233-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="50233-196">In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="50233-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="50233-198">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klik op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="50233-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="50233-200">Openen van de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="50233-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="50233-202">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="50233-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="50233-204">a.</span><span class="sxs-lookup"><span data-stu-id="50233-204">a.</span></span> <span data-ttu-id="50233-205">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="50233-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="50233-206">b.</span><span class="sxs-lookup"><span data-stu-id="50233-206">b.</span></span> <span data-ttu-id="50233-207">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="50233-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="50233-208">c.</span><span class="sxs-lookup"><span data-stu-id="50233-208">c.</span></span> <span data-ttu-id="50233-209">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="50233-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="50233-210">d.</span><span class="sxs-lookup"><span data-stu-id="50233-210">d.</span></span> <span data-ttu-id="50233-211">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="50233-211">Click **Create**.</span></span>
 
### <a name="creating-an-appdynamics-test-user"></a><span data-ttu-id="50233-212">Een testgebruiker AppDynamics maken</span><span class="sxs-lookup"><span data-stu-id="50233-212">Creating an AppDynamics test user</span></span>

<span data-ttu-id="50233-213">Om Azure AD-gebruikers zich aanmelden bij AppDynamics, moeten ze worden ingericht in AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="50233-213">To enable Azure AD users to log in to AppDynamics, they must be provisioned into AppDynamics.</span></span> <span data-ttu-id="50233-214">In het geval van AppDynamics is inrichting een handmatige taak.</span><span class="sxs-lookup"><span data-stu-id="50233-214">In the case of AppDynamics, provisioning is a manual task.</span></span>

<span data-ttu-id="50233-215">**Als u wilt configureren voor gebruikers inrichten, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="50233-215">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="50233-216">Meld u aan bij uw bedrijf AppDynamics site als beheerder.</span><span class="sxs-lookup"><span data-stu-id="50233-216">Log in to your AppDynamics company site as an administrator.</span></span>

2. <span data-ttu-id="50233-217">Ga naar **gebruikers**, en klik vervolgens op  **+**  openen de **gebruiker maken** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="50233-217">Go to **Users**, and then click **+** to open the **Create User** dialog.</span></span>
   
    <span data-ttu-id="50233-218">![Gebruikers](./media/active-directory-saas-appdynamics-tutorial/ic790229.png "gebruikers")</span><span class="sxs-lookup"><span data-stu-id="50233-218">![Users](./media/active-directory-saas-appdynamics-tutorial/ic790229.png "Users")</span></span>

3. <span data-ttu-id="50233-219">In de **gebruiker maken** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="50233-219">In the **Create User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="50233-220">![Gebruiker maken](./media/active-directory-saas-appdynamics-tutorial/ic790230.png "gebruiker maken")</span><span class="sxs-lookup"><span data-stu-id="50233-220">![Create User](./media/active-directory-saas-appdynamics-tutorial/ic790230.png "Create User")</span></span>
   
    <span data-ttu-id="50233-221">a.</span><span class="sxs-lookup"><span data-stu-id="50233-221">a.</span></span> <span data-ttu-id="50233-222">Typ de **gebruikersnaam**, **naam**, **e**, **nieuw wachtwoord**, **nieuw wachtwoord herhalen** van een geldige AAD account die u inrichten in de bijbehorende tekstvakken wilt.</span><span class="sxs-lookup"><span data-stu-id="50233-222">Type the **Username**, **Name**, **Email**, **New Password**, **Repeat New Password** of a valid AAD account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="50233-223">b.</span><span class="sxs-lookup"><span data-stu-id="50233-223">b.</span></span> <span data-ttu-id="50233-224">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="50233-224">Click **Save**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="50233-225">U kunt andere AppDynamics gebruiker account hulpmiddelen voor het maken of API's die is geleverd door AppDynamics voor het inrichten van Azure AD-gebruikersaccounts.</span><span class="sxs-lookup"><span data-stu-id="50233-225">You can use any other AppDynamics user account creation tools or APIs provided by AppDynamics to provision Azure AD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="50233-226">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="50233-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="50233-227">In deze sectie schakelt u Britta Simon gebruikt Azure eenmalige aanmelding toegang verlenen aan AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="50233-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AppDynamics.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="50233-229">**Britta Simon om aan te wijzen AppDynamics, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="50233-229">**To assign Britta Simon to AppDynamics, perform the following steps:**</span></span>

1. <span data-ttu-id="50233-230">Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="50233-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="50233-232">Selecteer in de lijst met toepassingen **AppDynamics**.</span><span class="sxs-lookup"><span data-stu-id="50233-232">In the applications list, select **AppDynamics**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_app.png) 

3. <span data-ttu-id="50233-234">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="50233-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="50233-236">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="50233-236">Click **Add** button.</span></span> <span data-ttu-id="50233-237">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="50233-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="50233-239">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="50233-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="50233-240">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="50233-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="50233-241">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="50233-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="50233-242">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="50233-242">Testing single sign-on</span></span>

<span data-ttu-id="50233-243">Het doel van deze sectie is het testen van uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="50233-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="50233-244">Als u op de tegel AppDynamics in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="50233-244">When you click the AppDynamics tile in the Access Panel, you should get automatically signed-on to your AppDynamics application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="50233-245">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="50233-245">Additional resources</span></span>

* [<span data-ttu-id="50233-246">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="50233-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="50233-247">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="50233-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_203.png

