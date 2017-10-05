---
title: 'Zelfstudie: Azure Active Directory-integratie met ServiceChannel | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en ServiceChannel.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c3546eab-96b5-489b-a309-b895eb428053
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/3/2017
ms.author: jeedes
ms.openlocfilehash: 7e1dad18ff0ae9a9102b789b2cb32e7b96ed3d38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicechannel"></a><span data-ttu-id="57dd4-103">Zelfstudie: Azure Active Directory-integratie met ServiceChannel</span><span class="sxs-lookup"><span data-stu-id="57dd4-103">Tutorial: Azure Active Directory integration with ServiceChannel</span></span>

<span data-ttu-id="57dd4-104">In deze zelfstudie leert u hoe ServiceChannel integreren met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="57dd4-104">In this tutorial, you learn how to integrate ServiceChannel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="57dd4-105">ServiceChannel integreren met Azure AD biedt de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="57dd4-105">Integrating ServiceChannel with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="57dd4-106">U kunt beheren in Azure AD die toegang tot ServiceChannel heeft</span><span class="sxs-lookup"><span data-stu-id="57dd4-106">You can control in Azure AD who has access to ServiceChannel</span></span>
- <span data-ttu-id="57dd4-107">U kunt uw gebruikers automatisch ophalen aangemeld bij ServiceChannel (Single Sign-On) met hun Azure AD-accounts inschakelen</span><span class="sxs-lookup"><span data-stu-id="57dd4-107">You can enable your users to automatically get signed-on to ServiceChannel (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="57dd4-108">U kunt uw accounts op één centrale locatie - en de Azure Management portal beheren</span><span class="sxs-lookup"><span data-stu-id="57dd4-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="57dd4-109">Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="57dd4-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57dd4-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="57dd4-110">Prerequisites</span></span>

<span data-ttu-id="57dd4-111">Voor het configureren van Azure AD-integratie met ServiceChannel, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="57dd4-111">To configure Azure AD integration with ServiceChannel, you need the following items:</span></span>

- <span data-ttu-id="57dd4-112">Een Azure AD-abonnement</span><span class="sxs-lookup"><span data-stu-id="57dd4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="57dd4-113">Een ServiceChannel eenmalige aanmelding ingeschakeld abonnement</span><span class="sxs-lookup"><span data-stu-id="57dd4-113">A ServiceChannel single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="57dd4-114">Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="57dd4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="57dd4-115">Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:</span><span class="sxs-lookup"><span data-stu-id="57dd4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="57dd4-116">U moet uw productieomgeving niet gebruiken tenzij dit noodzakelijk is.</span><span class="sxs-lookup"><span data-stu-id="57dd4-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="57dd4-117">Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u een proefversie van één maand [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="57dd4-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="57dd4-118">Scenariobeschrijving</span><span class="sxs-lookup"><span data-stu-id="57dd4-118">Scenario description</span></span>
<span data-ttu-id="57dd4-119">In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving.</span><span class="sxs-lookup"><span data-stu-id="57dd4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="57dd4-120">Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:</span><span class="sxs-lookup"><span data-stu-id="57dd4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="57dd4-121">ServiceChannel uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="57dd4-121">Adding ServiceChannel from the gallery</span></span>
2. <span data-ttu-id="57dd4-122">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="57dd4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-servicechannel-from-the-gallery"></a><span data-ttu-id="57dd4-123">ServiceChannel uit de galerie toevoegen</span><span class="sxs-lookup"><span data-stu-id="57dd4-123">Adding ServiceChannel from the gallery</span></span>
<span data-ttu-id="57dd4-124">Voor het configureren van de integratie van ServiceChannel in Azure AD, moet u ServiceChannel uit de galerie toevoegen aan de lijst met beheerde SaaS-apps.</span><span class="sxs-lookup"><span data-stu-id="57dd4-124">To configure the integration of ServiceChannel into Azure AD, you need to add ServiceChannel from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="57dd4-125">**Als u wilt toevoegen ServiceChannel uit de galerie, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="57dd4-125">**To add ServiceChannel from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="57dd4-126">In de  **[Azure Management Portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="57dd4-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="57dd4-128">Navigeer naar **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="57dd4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="57dd4-129">Ga vervolgens naar **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="57dd4-129">Then go to **All applications**.</span></span>

    ![Toepassingen][2]
    
3. <span data-ttu-id="57dd4-131">Klik op **toevoegen** knop boven aan het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="57dd4-131">Click **Add** button on the top of the dialog.</span></span>

    ![Toepassingen][3]

4. <span data-ttu-id="57dd4-133">Typ in het zoekvak **ServiceChannel**.</span><span class="sxs-lookup"><span data-stu-id="57dd4-133">In the search box, type **ServiceChannel**.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_000.png)

5. <span data-ttu-id="57dd4-135">Selecteer in het deelvenster resultaten **ServiceChannel**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="57dd4-135">In the results panel, select **ServiceChannel**, and then click **Add** button to add the application.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_2.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="57dd4-137">Configureren en testen van Azure AD eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="57dd4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="57dd4-138">In deze sectie configureert en test eenmalige aanmelding Azure AD met ServiceChannel op basis van een testgebruiker 'Britta Simon' genoemd.</span><span class="sxs-lookup"><span data-stu-id="57dd4-138">In this section, you configure and test Azure AD single sign-on with ServiceChannel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="57dd4-139">Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in ServiceChannel is voor een gebruiker in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="57dd4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ServiceChannel is to a user in Azure AD.</span></span> <span data-ttu-id="57dd4-140">Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de verwante ServiceChannel-gebruiker worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="57dd4-140">In other words, a link relationship between an Azure AD user and the related user in ServiceChannel needs to be established.</span></span>

<span data-ttu-id="57dd4-141">Deze relatie koppeling wordt ingesteld door het toewijzen van de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** in ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="57dd4-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ServiceChannel.</span></span>

<span data-ttu-id="57dd4-142">Om te configureren en testen van Azure AD eenmalige aanmelding met ServiceChannel, moet u de volgende bouwstenen voltooien:</span><span class="sxs-lookup"><span data-stu-id="57dd4-142">To configure and test Azure AD single sign-on with ServiceChannel, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="57dd4-143">**[Configureren van Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="57dd4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="57dd4-144">**[Maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="57dd4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="57dd4-145">**[Maken van een testgebruiker ServiceChannel](#creating-a-servicechannel-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="57dd4-145">**[Creating a ServiceChannel test user](#creating-a-servicechannel-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="57dd4-146">**[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.</span><span class="sxs-lookup"><span data-stu-id="57dd4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="57dd4-147">**[Testen van eenmalige aanmelding](#testing-single-sign-on)**  : om te controleren of de configuratie werkt.</span><span class="sxs-lookup"><span data-stu-id="57dd4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="57dd4-148">Eenmalige aanmelding Azure AD configureren</span><span class="sxs-lookup"><span data-stu-id="57dd4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="57dd4-149">In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure-beheerportal en eenmalige aanmelding in uw toepassing ServiceChannel configureren.</span><span class="sxs-lookup"><span data-stu-id="57dd4-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your ServiceChannel application.</span></span>

<span data-ttu-id="57dd4-150">**Voor het configureren van Azure AD eenmalige aanmelding met ServiceChannel, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="57dd4-150">**To configure Azure AD single sign-on with ServiceChannel, perform the following steps:**</span></span>

1. <span data-ttu-id="57dd4-151">In de Azure-beheerportal op de **ServiceChannel** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="57dd4-151">In the Azure Management portal, on the **ServiceChannel** application integration page, click **Single sign-on**.</span></span>

    ![Eenmalige aanmelding configureren][4]

2. <span data-ttu-id="57dd4-153">Op de **eenmalige aanmelding** dialoogvenster als **modus** Selecteer **op basis van SAML aanmelding** eenmalige aanmelding inschakelen op.</span><span class="sxs-lookup"><span data-stu-id="57dd4-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_01.png)

3. <span data-ttu-id="57dd4-155">Op de **ServiceChannel-domein en de URL's** sectie, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="57dd4-155">On the **ServiceChannel Domain and URLs** section, perform the following steps:</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_urls.png)

    <span data-ttu-id="57dd4-157">a.</span><span class="sxs-lookup"><span data-stu-id="57dd4-157">a.</span></span> <span data-ttu-id="57dd4-158">In de **id** textbox, typ de waarde als:`http://adfs.<domain>.com/adfs/service/trust`</span><span class="sxs-lookup"><span data-stu-id="57dd4-158">In the **Identifier** textbox, type the value as: `http://adfs.<domain>.com/adfs/service/trust`</span></span>

    <span data-ttu-id="57dd4-159">b.</span><span class="sxs-lookup"><span data-stu-id="57dd4-159">b.</span></span> <span data-ttu-id="57dd4-160">In de **antwoord-URL** textbox, typ een URL met het volgende patroon volgen:`https://<customer domain>.servicechannel.com/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="57dd4-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<customer domain>.servicechannel.com/saml/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="57dd4-161">Houd er rekening mee dat deze niet de werkelijke waarden zijn.</span><span class="sxs-lookup"><span data-stu-id="57dd4-161">Please note that these are not the real values.</span></span> <span data-ttu-id="57dd4-162">U hebt deze waarden bijwerken met de werkelijke id en de antwoord-URL.</span><span class="sxs-lookup"><span data-stu-id="57dd4-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="57dd4-163">Hier raden we u voor het gebruik van de unieke waarde van een tekenreeks in de id.</span><span class="sxs-lookup"><span data-stu-id="57dd4-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="57dd4-164">Neem contact op met [ServiceChannel ondersteuningsteam](https://servicechannel.zendesk.com/hc/en-us) ophalen van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="57dd4-164">Contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us) to get these values.</span></span>

4. <span data-ttu-id="57dd4-165">Uw toepassing ServiceChannel verwacht de SAML-asserties in een specifieke indeling waarvoor u aangepaste kenmerktoewijzingen toevoegen aan uw configuratie van SAML-token kenmerken.</span><span class="sxs-lookup"><span data-stu-id="57dd4-165">Your ServiceChannel application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="57dd4-166">De volgende Schermafbeelding toont een voorbeeld voor deze.</span><span class="sxs-lookup"><span data-stu-id="57dd4-166">The following screenshot shows an example for this.</span></span> <span data-ttu-id="57dd4-167">**NameIdentifier (gebruikers-id)** is het alleen verplichte claim en de standaardwaarde is **user.userprincipalname** maar ServiceChannel verwacht deze optie om te worden toegewezen met **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="57dd4-167">**NameIdentifier(User Identifier)** is the only mandatory claim and the default value is **user.userprincipalname** but ServiceChannel expects this to be mapped with **user.mail**.</span></span> <span data-ttu-id="57dd4-168">Als u van plan bent om in te schakelen NET In Time gebruikers inrichten, moet u de volgende claims toevoegen zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="57dd4-168">If you are planning to enable Just In Time user provisioning, then you should add the following claims as shown below.</span></span> <span data-ttu-id="57dd4-169">**Rol** claim moet worden toegewezen aan **user.assignedroles** die de rol van de gebruiker bevat.</span><span class="sxs-lookup"><span data-stu-id="57dd4-169">**Role** claim needs to be mapped to **user.assignedroles** which contains the role of the user.</span></span>  

    <span data-ttu-id="57dd4-170">U kunt verwijzen ServiceChannel handleiding [hier](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) voor meer informatie over claims.</span><span class="sxs-lookup"><span data-stu-id="57dd4-170">You can refer ServiceChannel guide [here](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) for more guidance on claims.</span></span>
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_attribute.png)

    > [!NOTE] 
    > <span data-ttu-id="57dd4-172">Klik op de [hier](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) weten hoe u configureert **rol** in Azure AD</span><span class="sxs-lookup"><span data-stu-id="57dd4-172">Please click [here](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) to know how to configure **Role** in Azure AD</span></span>

5. <span data-ttu-id="57dd4-173">In **gebruikerskenmerken** sectie, klikt u op **weergeven en bewerken van alle andere gebruikerskenmerken** en kenmerken instellen.</span><span class="sxs-lookup"><span data-stu-id="57dd4-173">In **User Attributes** section, click **View and edit all other user attributes** and set the attributes.</span></span>

    | <span data-ttu-id="57dd4-174">Naam van kenmerk</span><span class="sxs-lookup"><span data-stu-id="57dd4-174">Attribute Name</span></span> | <span data-ttu-id="57dd4-175">De waarde van kenmerk</span><span class="sxs-lookup"><span data-stu-id="57dd4-175">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="57dd4-176">Rol</span><span class="sxs-lookup"><span data-stu-id="57dd4-176">Role</span></span>| <span data-ttu-id="57dd4-177">User.assignedroles</span><span class="sxs-lookup"><span data-stu-id="57dd4-177">user.assignedroles</span></span> |

    <span data-ttu-id="57dd4-178">a.</span><span class="sxs-lookup"><span data-stu-id="57dd4-178">a.</span></span> <span data-ttu-id="57dd4-179">Klik op **toevoegen kenmerk** openen de **kenmerk toevoegen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="57dd4-179">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_05.png)
    
    <span data-ttu-id="57dd4-182">b.</span><span class="sxs-lookup"><span data-stu-id="57dd4-182">b.</span></span> <span data-ttu-id="57dd4-183">In de **naam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="57dd4-183">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="57dd4-184">c.</span><span class="sxs-lookup"><span data-stu-id="57dd4-184">c.</span></span> <span data-ttu-id="57dd4-185">Van de **waarde** typt u de waarde van het kenmerk wordt weergegeven voor die rij.</span><span class="sxs-lookup"><span data-stu-id="57dd4-185">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="57dd4-186">d.</span><span class="sxs-lookup"><span data-stu-id="57dd4-186">d.</span></span> <span data-ttu-id="57dd4-187">Klik op **Ok**</span><span class="sxs-lookup"><span data-stu-id="57dd4-187">Click **Ok**</span></span>
    
6. <span data-ttu-id="57dd4-188">Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **certificaat (Base64)** en sla het certificaatbestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="57dd4-188">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_05.png) 

7. <span data-ttu-id="57dd4-190">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="57dd4-190">Click **Save**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicechannel-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="57dd4-192">Op de **ServiceChannel configuratie** sectie, klikt u op **configureren ServiceChannel** openen **eenmalige aanmelding configureren** venster.</span><span class="sxs-lookup"><span data-stu-id="57dd4-192">On the **ServiceChannel Configuration** section, click **Configure ServiceChannel** to open **Configure sign-on** window.</span></span> <span data-ttu-id="57dd4-193">Houd rekening met de **SAML Enitity ID** van de **Naslaggids** sectie.</span><span class="sxs-lookup"><span data-stu-id="57dd4-193">Please note the **SAML Enitity ID** from the **Quick Reference** section.</span></span>

9. <span data-ttu-id="57dd4-194">Eenmalige aanmelding configureren op **ServiceChannel** zijde, moet u de gedownloade verzenden **certificaat (Base64)** en **SAML entiteit-ID** naar [ServiceChannel ondersteuningsteam](https://servicechannel.zendesk.com/hc/en-us).</span><span class="sxs-lookup"><span data-stu-id="57dd4-194">To configure single sign-on on **ServiceChannel** side, you need to send the downloaded **certificate (Base64)** and **SAML Entity ID** to [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us).</span></span> <span data-ttu-id="57dd4-195">Ze zullen dit instellen om de SAML SSO-verbinding juist is ingesteld op beide zijden.</span><span class="sxs-lookup"><span data-stu-id="57dd4-195">They will set this up in order to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="57dd4-196">Een Azure AD-testgebruiker maken</span><span class="sxs-lookup"><span data-stu-id="57dd4-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="57dd4-197">Het doel van deze sectie is het een testgebruiker maken in Azure Management portal Britta Simon aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="57dd4-197">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Azure AD-gebruiker maken][100]

<span data-ttu-id="57dd4-199">**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="57dd4-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="57dd4-200">In de **Azure Management portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.</span><span class="sxs-lookup"><span data-stu-id="57dd4-200">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="57dd4-202">Ga naar **gebruikers en groepen** en klik op **alle gebruikers** om de lijst met gebruikers weer te geven.</span><span class="sxs-lookup"><span data-stu-id="57dd4-202">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="57dd4-204">Klik aan de bovenkant van het dialoogvenster **toevoegen** openen de **gebruiker** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="57dd4-204">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="57dd4-206">Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="57dd4-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Een Azure AD-testgebruiker maken](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="57dd4-208">a.</span><span class="sxs-lookup"><span data-stu-id="57dd4-208">a.</span></span> <span data-ttu-id="57dd4-209">In de **naam** textbox type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="57dd4-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="57dd4-210">b.</span><span class="sxs-lookup"><span data-stu-id="57dd4-210">b.</span></span> <span data-ttu-id="57dd4-211">In de **gebruikersnaam** textbox type de **e-mailadres** van BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="57dd4-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="57dd4-212">c.</span><span class="sxs-lookup"><span data-stu-id="57dd4-212">c.</span></span> <span data-ttu-id="57dd4-213">Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.</span><span class="sxs-lookup"><span data-stu-id="57dd4-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="57dd4-214">d.</span><span class="sxs-lookup"><span data-stu-id="57dd4-214">d.</span></span> <span data-ttu-id="57dd4-215">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="57dd4-215">Click **Create**.</span></span> 

### <a name="creating-a-servicechannel-test-user"></a><span data-ttu-id="57dd4-216">Een testgebruiker ServiceChannel maken</span><span class="sxs-lookup"><span data-stu-id="57dd4-216">Creating a ServiceChannel test user</span></span>

<span data-ttu-id="57dd4-217">Toepassing ondersteunt Just in tijd gebruikers inrichten en na verificatie gebruikers wordt in de toepassing automatisch gemaakt.</span><span class="sxs-lookup"><span data-stu-id="57dd4-217">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> <span data-ttu-id="57dd4-218">Voor volledige gebruikersinrichting, neem contact op met [ondersteuningsteam ServiceChannel](https://servicechannel.zendesk.com/hc/en-us)</span><span class="sxs-lookup"><span data-stu-id="57dd4-218">For full user provisioning, please contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us)</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="57dd4-219">Toewijzen van de testgebruiker Azure AD</span><span class="sxs-lookup"><span data-stu-id="57dd4-219">Assigning the Azure AD test user</span></span>

<span data-ttu-id="57dd4-220">In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door haar toegang verlenen aan ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="57dd4-220">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to ServiceChannel.</span></span>

![Gebruiker toewijzen][200] 

<span data-ttu-id="57dd4-222">**Britta Simon om aan te wijzen ServiceChannel, moet u de volgende stappen uitvoeren:**</span><span class="sxs-lookup"><span data-stu-id="57dd4-222">**To assign Britta Simon to ServiceChannel, perform the following steps:**</span></span>

1. <span data-ttu-id="57dd4-223">In de Azure-beheerportal, opent u de weergave toepassingen en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="57dd4-223">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Gebruiker toewijzen][201] 

2. <span data-ttu-id="57dd4-225">Selecteer in de lijst met toepassingen **ServiceChannel**.</span><span class="sxs-lookup"><span data-stu-id="57dd4-225">In the applications list, select **ServiceChannel**.</span></span>

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_app01.png) 

3. <span data-ttu-id="57dd4-227">Klik in het menu aan de linkerkant op **gebruikers en groepen**.</span><span class="sxs-lookup"><span data-stu-id="57dd4-227">In the menu on the left, click **Users and groups**.</span></span>

    ![Gebruiker toewijzen][202] 

4. <span data-ttu-id="57dd4-229">Klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="57dd4-229">Click **Add** button.</span></span> <span data-ttu-id="57dd4-230">Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="57dd4-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Gebruiker toewijzen][203]

5. <span data-ttu-id="57dd4-232">Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.</span><span class="sxs-lookup"><span data-stu-id="57dd4-232">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="57dd4-233">Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="57dd4-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="57dd4-234">Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="57dd4-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="57dd4-235">Testen van eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="57dd4-235">Testing single sign-on</span></span>

<span data-ttu-id="57dd4-236">In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.</span><span class="sxs-lookup"><span data-stu-id="57dd4-236">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="57dd4-237">Als u op de tegel ServiceChannel in het deelvenster toegang, u moet ophalen automatisch aangemeld bij uw toepassing ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="57dd4-237">When you click the ServiceChannel tile in the Access Panel, you should get automatically signed-on to your ServiceChannel application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="57dd4-238">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="57dd4-238">Additional resources</span></span>

* [<span data-ttu-id="57dd4-239">Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="57dd4-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="57dd4-240">Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="57dd4-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_203.png