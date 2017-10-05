---
title: "Zelfstudie: Azure Active Directory-integratie met IBM Kenexa enquête Enterprise | Microsoft Docs"
description: "Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en IBM Kenexa enquête Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c7aac6da-f4bf-419e-9e1a-16b460641a52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 5c276c23288292a1c54dd9d57177d5072b90c9e3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ibm-kenexa-survey-enterprise"></a><span data-ttu-id="dea3e-103">Zelfstudie: Azure Active Directory-integratie met IBM Kenexa enquête Enterprise</span><span class="sxs-lookup"><span data-stu-id="dea3e-103">Tutorial: Azure Active Directory integration with IBM Kenexa Survey Enterprise</span></span>

<span data-ttu-id="dea3e-104">In deze zelfstudie leert u hoe IBM Kenexa enquête Enterprise integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dea3e-104">In this tutorial, you learn how to integrate IBM Kenexa Survey Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dea3e-105">IBM Kenexa enquête Enterprise integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="dea3e-105">Integrating IBM Kenexa Survey Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="dea3e-106">U kunt beheren in Azure AD die toegang tot IBM Kenexa enquête Enterprise heeft.</span><span class="sxs-lookup"><span data-stu-id="dea3e-106">You can control in Azure AD who has access to IBM Kenexa Survey Enterprise.</span></span>
- <span data-ttu-id="dea3e-107">U kunt uw gebruikers automatisch aanmelden bij IBM Kenexa enquête Enterprise met behulp van eenmalige aanmelding (SSO) met hun Azure AD-accounts kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="dea3e-107">You can enable your users to automatically sign in to IBM Kenexa Survey Enterprise by using single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="dea3e-108">U kunt uw accounts op één locatie beheren: de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="dea3e-108">You can manage your accounts in one central location: the Azure portal.</span></span>

<span data-ttu-id="dea3e-109">Als u meer weten over software als een dienst (SaaS)-app-integratie met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dea3e-109">If you want to know more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dea3e-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="dea3e-110">Prerequisites</span></span>

<span data-ttu-id="dea3e-111">Voor het configureren van Azure AD-integratie met IBM Kenexa enquête voor ondernemingen, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="dea3e-111">To configure Azure AD integration with IBM Kenexa Survey Enterprise, you need the following items:</span></span>

- <span data-ttu-id="dea3e-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="dea3e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dea3e-113">Een abonnement IBM Kenexa enquête Enterprise SSO-ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="dea3e-113">An IBM Kenexa Survey Enterprise SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dea3e-114">Wanneer u de stappen in deze zelfstudie test, wordt u aangeraden een productie-omgeving niet te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="dea3e-114">When you test the steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="dea3e-115">Test de stappen in deze zelfstudie, volgt u deze aanbevelingen:</span><span class="sxs-lookup"><span data-stu-id="dea3e-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="dea3e-116">Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="dea3e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dea3e-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dea3e-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dea3e-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="dea3e-118">Scenario description</span></span>
<span data-ttu-id="dea3e-119">In deze zelfstudie kunt u Azure AD SSO testen in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="dea3e-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="dea3e-120">Het scenario in de zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="dea3e-120">The scenario outlined in the tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="dea3e-121">IBM Kenexa enquête Enterprise uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="dea3e-121">Adding IBM Kenexa Survey Enterprise from the gallery</span></span>
* <span data-ttu-id="dea3e-122">Configureren en testen van Azure AD-SSO</span><span class="sxs-lookup"><span data-stu-id="dea3e-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-ibm-kenexa-survey-enterprise-from-the-gallery"></a><span data-ttu-id="dea3e-123">IBM Kenexa enquête Enterprise uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="dea3e-123">Add IBM Kenexa Survey Enterprise from the gallery</span></span>
<span data-ttu-id="dea3e-124">Voor het configureren van de integratie van IBM Kenexa enquête Enterprise in Azure AD IBM Kenexa enquête Enterprise uit de galerie te toevoegt aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="dea3e-124">To configure the integration of IBM Kenexa Survey Enterprise into Azure AD, add IBM Kenexa Survey Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="dea3e-125">Als u wilt toevoegen IBM Kenexa enquête Enterprise uit de galerie, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="dea3e-125">To add IBM Kenexa Survey Enterprise from the gallery, do the following:</span></span>

1. <span data-ttu-id="dea3e-126">In de [Azure-portal](https://portal.azure.com), in het linkerdeelvenster klikt u op de **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="dea3e-126">In the [Azure portal](https://portal.azure.com), in the left pane, click the **Azure Active Directory** button.</span></span> 

    ![De Azure Active Directory-knop][1]

2. <span data-ttu-id="dea3e-128">Selecteer **bedrijfstoepassingen**, en selecteer vervolgens **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="dea3e-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![De blade Enterprise-toepassingen][2]
    
3. <span data-ttu-id="dea3e-130">Als u wilt een toepassing toevoegen, klikt u op de **nieuwe toepassing** knop.</span><span class="sxs-lookup"><span data-stu-id="dea3e-130">To add an application, click the **New application** button.</span></span>

    ![De knop Nieuw toepassing][3]

4. <span data-ttu-id="dea3e-132">Typ in het zoekvak **IBM Kenexa enquête Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="dea3e-132">In the search box, type **IBM Kenexa Survey Enterprise**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_search.png)

5. <span data-ttu-id="dea3e-134">Selecteer in de lijst met resultaten **IBM Kenexa enquête Enterprise**, en klik vervolgens op de **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="dea3e-134">In the results list, select **IBM Kenexa Survey Enterprise**, and then click the **Add** button to add the application.</span></span>

    ![IBM Kenexa enquête onderneming in de lijst met resultaten](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="dea3e-136">Configureren en testen eenmalige aanmelding Azure AD</span><span class="sxs-lookup"><span data-stu-id="dea3e-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="dea3e-137">In deze sectie kunt u configureren en testen van Azure AD-SSO met IBM Kenexa enquête Enterprise op basis van een testgebruiker genaamd "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="dea3e-137">In this section, you configure and test Azure AD SSO with IBM Kenexa Survey Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="dea3e-138">Azure AD moet de gebruiker IBM Kenexa enquête Enterprise equivalent identificeren in Azure AD voor eenmalige aanmelding werkt.</span><span class="sxs-lookup"><span data-stu-id="dea3e-138">For SSO to work, Azure AD needs to identify the IBM Kenexa Survey Enterprise user counterpart in Azure AD.</span></span> <span data-ttu-id="dea3e-139">Azure AD moet met andere woorden, een koppeling relatie tussen een Azure AD-gebruiker en een bijbehorende gebruiker maken in IBM Kenexa enquête onderneming.</span><span class="sxs-lookup"><span data-stu-id="dea3e-139">In other words, Azure AD must establish a link relationship between an Azure AD user and a related user in IBM Kenexa Survey Enterprise.</span></span>

<span data-ttu-id="dea3e-140">Om vast te stellen op de koppeling relatie, wijs de waarde van de **gebruikersnaam** in IBM Kenexa enquête Enterprise als de waarde van de **gebruikersnaam** in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dea3e-140">To establish the link relationship, assign the value of the **user name** in IBM Kenexa Survey Enterprise as the value of the **Username** in Azure AD.</span></span>

<span data-ttu-id="dea3e-141">Als u wilt configureren en testen van Azure AD-SSO met IBM Kenexa enquête Enterprise, voltooi de bouwstenen in de volgende twee secties.</span><span class="sxs-lookup"><span data-stu-id="dea3e-141">To configure and test Azure AD SSO with IBM Kenexa Survey Enterprise, complete the building blocks in the next two sections.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="dea3e-142">Azure AD-eenmalige aanmelding configureren</span><span class="sxs-lookup"><span data-stu-id="dea3e-142">Configure Azure AD SSO</span></span>

<span data-ttu-id="dea3e-143">In dit gedeelte Azure AD-eenmalige aanmelding inschakelen in de Azure-portal en eenmalige aanmelding in uw toepassing IBM Kenexa enquête Enterprise als volgt configureren:</span><span class="sxs-lookup"><span data-stu-id="dea3e-143">In this section, you enable Azure AD SSO in the Azure portal and configure SSO in your IBM Kenexa Survey Enterprise application by doing the following:</span></span>

1. <span data-ttu-id="dea3e-144">In de Azure-portal op de **IBM Kenexa enquête Enterprise** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="dea3e-144">In the Azure portal, on the **IBM Kenexa Survey Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![IBM Kenexa enquête Enterprise configureren één aanmelding koppeling][4]

2. <span data-ttu-id="dea3e-146">In de **eenmalige aanmelding** het dialoogvenster de **modus** de optie **op basis van SAML aanmelding** eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="dea3e-146">In the **Single sign-on** dialog box, in the **Mode** box, select **SAML-based Sign-on** to enable SSO.</span></span>
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_samlbase.png)

3. <span data-ttu-id="dea3e-148">In de **IBM Kenexa enquête Enterprise domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="dea3e-148">In the **IBM Kenexa Survey Enterprise Domain and URLs** section, perform the following steps:</span></span>

    ![IBM Kenexa enquête Enterprise domein en de URL's van eenmalige aanmelding informatie](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_url.png)

    <span data-ttu-id="dea3e-150">a.</span><span class="sxs-lookup"><span data-stu-id="dea3e-150">a.</span></span> <span data-ttu-id="dea3e-151">In de **id** textbox type een URL met het volgende patroon volgen:`https://surveys.kenexa.com/<companycode>`</span><span class="sxs-lookup"><span data-stu-id="dea3e-151">In the **Identifier** textbox, type a URL with the following pattern: `https://surveys.kenexa.com/<companycode>`</span></span>

    <span data-ttu-id="dea3e-152">b.</span><span class="sxs-lookup"><span data-stu-id="dea3e-152">b.</span></span> <span data-ttu-id="dea3e-153">In de **antwoord-URL** textbox type een URL met het volgende patroon volgen:`https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span><span class="sxs-lookup"><span data-stu-id="dea3e-153">In the **Reply URL** textbox, type a URL with the following pattern: `https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dea3e-154">De voorgaande waarden zijn niet echt.</span><span class="sxs-lookup"><span data-stu-id="dea3e-154">The preceding values are not real.</span></span> <span data-ttu-id="dea3e-155">Deze bijwerken met de werkelijke-id en antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="dea3e-155">Update them with the actual identifier and reply URL.</span></span> <span data-ttu-id="dea3e-156">De werkelijke waarden, neem contact op met de [IBM Kenexa enquête Enterprise ondersteuningsteam](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="dea3e-156">To obtain the actual values, contact the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

4. <span data-ttu-id="dea3e-157">Onder **SAML-certificaat voor ondertekening van**, klikt u op **certificaat (Base64)**, en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="dea3e-157">Under **SAML Signing Certificate**, click **Certificate (Base64)**, and then save the certificate file to your computer.</span></span>

    ![De downloadkoppeling certificaat (Base64)](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_certificate.png) 

    <span data-ttu-id="dea3e-159">De bedrijfstoepassing IBM Kenexa enquête verwacht te ontvangen van de asserties Security Asserties Markup Language (SAML) in een specifieke indeling waarvoor u aangepaste kenmerktoewijzingen toevoegen aan de configuratie van de kenmerken van SAML-token.</span><span class="sxs-lookup"><span data-stu-id="dea3e-159">The IBM Kenexa Survey Enterprise application expects to receive the Security Assertions Markup Language (SAML) assertions in a specific format, which requires you to add custom attribute mappings to the configuration of your SAML token attributes.</span></span> <span data-ttu-id="dea3e-160">De waarde van de claim gebruiker-id in het antwoord moet overeenkomen met de ID voor eenmalige aanmelding die geconfigureerd in het systeem Kenexa.</span><span class="sxs-lookup"><span data-stu-id="dea3e-160">The value of the user-identifier claim in the response must match the SSO ID that's configured in the Kenexa system.</span></span> <span data-ttu-id="dea3e-161">Als u wilt toewijzen in de juiste gebruikers-id in uw organisatie als SSO Internet Datagram Protocol (IDP), werkt u met de [IBM Kenexa enquête Enterprise ondersteuningsteam](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="dea3e-161">To map the appropriate user identifier in your organization as SSO Internet Datagram Protocol (IDP), work with the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> 

    <span data-ttu-id="dea3e-162">Azure AD wordt standaard ingesteld van de gebruikers-id als de waarde van de principal-naam (User Principal Name) gebruiker.</span><span class="sxs-lookup"><span data-stu-id="dea3e-162">By default, Azure AD sets the user identifier as the user principal name (UPN) value.</span></span> <span data-ttu-id="dea3e-163">U kunt deze waarde wijzigen op de **kenmerk** tabblad, zoals wordt weergegeven in de volgende schermafbeelding.</span><span class="sxs-lookup"><span data-stu-id="dea3e-163">You can change this value on the **Attribute** tab, as shown in the following screenshot.</span></span> <span data-ttu-id="dea3e-164">De integratie werkt alleen na voltooiing van de toewijzing correct.</span><span class="sxs-lookup"><span data-stu-id="dea3e-164">The integration works only after you've completed the mapping correctly.</span></span>
    
    ![Het dialoogvenster gebruikerskenmerken](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_attribute.png)   

5. <span data-ttu-id="dea3e-166">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="dea3e-166">Click **Save**.</span></span>

    ![De configureren eenmalige aanmelding knop Opslaan](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dea3e-168">Openen van de **eenmalige aanmelding configureren** venster onder **IBM Kenexa enquête Enterprise Configuration**, klikt u op **configureren IBM Kenexa enquête Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="dea3e-168">To open the **Configure sign-on** window, under **IBM Kenexa Survey Enterprise Configuration**, click **Configure IBM Kenexa Survey Enterprise**.</span></span> 
 
    ![De koppeling IBM Kenexa enquête Enterprise configureren](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_configure.png)

7. <span data-ttu-id="dea3e-170">Kopieer de **Sign-Out URL**, **SAML entiteit-ID**, en **SAML aanmelding Service-URL met eenmalige** waarden van de **Naslaggids** sectie.</span><span class="sxs-lookup"><span data-stu-id="dea3e-170">Copy the **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values from the **Quick Reference** section.</span></span>

8. <span data-ttu-id="dea3e-171">In de **eenmalige aanmelding configureren** venster onder **Naslaggids**, Kopieer de **Sign-Out URL**, **SAML entiteit-ID**, en **SAML eenmalige aanmelding Service-URL** waarden.</span><span class="sxs-lookup"><span data-stu-id="dea3e-171">In the **Configure sign-on** window, under **Quick Reference**, copy the **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values.</span></span>

9. <span data-ttu-id="dea3e-172">Eenmalige aanmelding configureren op de **IBM Kenexa enquête Enterprise** zijde, verzenden de gedownloade **certificaat (Base64)**, **Sign-Out URL**, **SAML entiteit-ID**, en **SAML één Service-URL aanmelding** waarden voor de [IBM Kenexa enquête Enterprise ondersteuningsteam](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="dea3e-172">To configure SSO on the **IBM Kenexa Survey Enterprise** side, send the downloaded **Certificate (Base64)**, **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values to the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

> [!TIP]
> <span data-ttu-id="dea3e-173">U kunt verwijzen naar een beknopte versie van deze instructies in de [Azure-portal](https://portal.azure.com) tijdens het instellen van de app.</span><span class="sxs-lookup"><span data-stu-id="dea3e-173">You can refer to a concise version of these instructions in the [Azure portal](https://portal.azure.com) while you are setting up the app.</span></span> <span data-ttu-id="dea3e-174">Na het toevoegen van de app vanuit de **Active Directory** > **bedrijfstoepassingen** sectie, klikt u op de **eenmalige aanmelding** tabblad en vervolgens naar de Embedded-documentatie via de **configuratie** sectie aan het einde.</span><span class="sxs-lookup"><span data-stu-id="dea3e-174">After you add the app from the **Active Directory** > **Enterprise Applications** section, simply click the **single sign-on** tab, and then access the embedded documentation through the **Configuration** section at the end.</span></span> <span data-ttu-id="dea3e-175">Zie voor meer informatie over de functie embedded-documentatie, [documentatie van Azure AD ingesloten](https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="dea3e-175">To learn more about the embedded documentation feature, see [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="dea3e-176">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="dea3e-176">Create an Azure AD test user</span></span>
<span data-ttu-id="dea3e-177">In deze sectie kunt u testgebruiker Britta Simon in de Azure portal maken door het volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="dea3e-177">In this section, you create test user Britta Simon in the Azure portal by doing the following:</span></span>

![Een Azure AD-testgebruiker maken][100]

1. <span data-ttu-id="dea3e-179">Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.</span><span class="sxs-lookup"><span data-stu-id="dea3e-179">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![De Azure Active Directory-knop](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dea3e-181">Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="dea3e-181">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>
    
    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dea3e-183">Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="dea3e-183">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>
 
    ![De knop toevoegen](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dea3e-185">In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="dea3e-185">In the **User** dialog box, perform the following steps:</span></span>
 
    ![Het dialoogvenster gebruiker](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dea3e-187">a.</span><span class="sxs-lookup"><span data-stu-id="dea3e-187">a.</span></span> <span data-ttu-id="dea3e-188">In de **naam** in het vak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dea3e-188">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dea3e-189">b.</span><span class="sxs-lookup"><span data-stu-id="dea3e-189">b.</span></span> <span data-ttu-id="dea3e-190">In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dea3e-190">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="dea3e-191">c.</span><span class="sxs-lookup"><span data-stu-id="dea3e-191">c.</span></span> <span data-ttu-id="dea3e-192">Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.</span><span class="sxs-lookup"><span data-stu-id="dea3e-192">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="dea3e-193">d.</span><span class="sxs-lookup"><span data-stu-id="dea3e-193">d.</span></span> <span data-ttu-id="dea3e-194">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="dea3e-194">Click **Create**.</span></span>
 
### <a name="create-an-ibm-kenexa-survey-enterprise-test-user"></a><span data-ttu-id="dea3e-195">Een IBM Kenexa enquête Enterprise testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="dea3e-195">Create an IBM Kenexa Survey Enterprise test user</span></span>

<span data-ttu-id="dea3e-196">In deze sectie kunt u een gebruiker met de naam van Britta Simon in IBM Kenexa enquête onderneming maken.</span><span class="sxs-lookup"><span data-stu-id="dea3e-196">In this section, you create a user called Britta Simon in IBM Kenexa Survey Enterprise.</span></span> 

<span data-ttu-id="dea3e-197">Als u wilt maken van gebruikers in het systeem IBM Kenexa enquête Enterprise en de SSO-ID voor deze toewijst, kunt u samenwerken met de [IBM Kenexa enquête Enterprise ondersteuningsteam](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="dea3e-197">To create users in the IBM Kenexa Survey Enterprise system and map the SSO ID for them, you can work with the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> <span data-ttu-id="dea3e-198">Deze SSO-ID-waarde moet ook worden toegewezen aan de waarde van de gebruiker-id van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dea3e-198">This SSO ID value should also be mapped to the user identifier value from Azure AD.</span></span> <span data-ttu-id="dea3e-199">U kunt deze standaardinstelling wijzigen op de **kenmerk** tabblad.</span><span class="sxs-lookup"><span data-stu-id="dea3e-199">You can change this default setting on the **Attribute** tab.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="dea3e-200">De Azure AD-testgebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="dea3e-200">Assign the Azure AD test user</span></span>

<span data-ttu-id="dea3e-201">In deze sectie schakelt u de gebruiker Britta Simon Azure SSO toegang verleent tot IBM Kenexa enquête onderneming gebruiken.</span><span class="sxs-lookup"><span data-stu-id="dea3e-201">In this section, you enable user Britta Simon to use Azure SSO by granting access to IBM Kenexa Survey Enterprise.</span></span>

![Toewijzen van de gebruikersrol][200] 

<span data-ttu-id="dea3e-203">Gebruiker Britta Simon om aan te wijzen IBM Kenexa enquête Enterprise, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="dea3e-203">To assign user Britta Simon to IBM Kenexa Survey Enterprise, do the following:</span></span>

1. <span data-ttu-id="dea3e-204">Open in de Azure-portal, de **toepassingen** weergeven, gaat u naar de **Directory** weergave, selecteer **bedrijfstoepassingen**, en klik vervolgens op **alle toepassingen** .</span><span class="sxs-lookup"><span data-stu-id="dea3e-204">In the Azure portal, open the **Applications** view, go to the **Directory** view, select **Enterprise applications**, and then click **All applications**.</span></span>

    ![De 'Bedrijfstoepassingen' en 'Alle toepassingen' koppelingen][201] 

2. <span data-ttu-id="dea3e-206">In de **toepassingen** selecteert **IBM Kenexa enquête Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="dea3e-206">In the **Applications** list, select **IBM Kenexa Survey Enterprise**.</span></span>

    ![De IBM Kenexa enquête Enterprise-koppeling in de lijst met toepassingen](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_app.png) 

3. <span data-ttu-id="dea3e-208">Klik in het linkerdeelvenster op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="dea3e-208">In the left pane, click **Users and groups**.</span></span>

    ![De koppeling 'Gebruikers en groepen'][202] 

4. <span data-ttu-id="dea3e-210">Klik op de **toevoegen** knop en klikt u op de **toevoegen toewijzing** deelvenster **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="dea3e-210">Click the **Add** button and then, in the **Add Assignment** pane, select **Users and groups**.</span></span>

    ![Het deelvenster toewijzing toevoegen][203]

5. <span data-ttu-id="dea3e-212">In de **gebruikers en groepen** het dialoogvenster de **gebruikers** selecteert **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="dea3e-212">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="dea3e-213">In de **gebruikers en groepen** in het dialoogvenster, klikt u op de **Selecteer** knop.</span><span class="sxs-lookup"><span data-stu-id="dea3e-213">In the **Users and groups** dialog box, click the **Select** button.</span></span>

7. <span data-ttu-id="dea3e-214">In de **toevoegen toewijzing** in het dialoogvenster, klikt u op de **toewijzen** knop.</span><span class="sxs-lookup"><span data-stu-id="dea3e-214">In the **Add Assignment** dialog box, click the **Assign** button.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="dea3e-215">Test eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="dea3e-215">Test single sign-on</span></span>

<span data-ttu-id="dea3e-216">In deze sectie kunt u de configuratie van uw Azure AD SSO testen met behulp van het toegangsvenster.</span><span class="sxs-lookup"><span data-stu-id="dea3e-216">In this section, you test your Azure AD SSO configuration by using the Access Panel.</span></span>

<span data-ttu-id="dea3e-217">Wanneer u klikt op de **IBM Kenexa enquête Enterprise** tegel in het deelvenster toegang u moet worden automatisch aangemeld bij uw toepassing IBM Kenexa enquête Enterprise.</span><span class="sxs-lookup"><span data-stu-id="dea3e-217">When you click the **IBM Kenexa Survey Enterprise** tile in the Access Panel, you should be automatically signed in to your IBM Kenexa Survey Enterprise application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dea3e-218">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="dea3e-218">Additional resources</span></span>

* [<span data-ttu-id="dea3e-219">Lijst met zelfstudies over het integreren van SaaS-apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dea3e-219">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dea3e-220">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dea3e-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_203.png

 
