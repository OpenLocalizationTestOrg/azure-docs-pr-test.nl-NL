---
title: Wat is er nieuw in Enterprise Toepassingsbeheer in Azure Active Directory | Microsoft Docs
description: Ontdek wat er nieuw in Enterprise Toepassingsbeheer in Azure Active Directory.
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
editor: 
ms.assetid: 34ac4028-a5aa-40d9-a93b-0db4e0abd793
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: asteen
ms.reviewer: asteen
ms.openlocfilehash: 0c32a6719292aa903aa32dfdc4a31114e7a28346
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="whats-new-in-enterprise-application-management-in-azure-active-directory"></a><span data-ttu-id="2803f-103">Wat is er nieuw in Enterprise Toepassingsbeheer in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2803f-103">What's new in Enterprise Application management in Azure Active Directory</span></span> 

<span data-ttu-id="2803f-104">Azure Active Directory (Azure AD) is uitgebreid enterprise hulpprogramma's voor toepassingsbeheer, met nieuwe functies en mogelijkheden voor het maken van het beheer van apps eenvoudiger en efficiënter.</span><span class="sxs-lookup"><span data-stu-id="2803f-104">Azure Active Directory (Azure AD) has enhanced enterprise application management tools, with new features and capabilities to make managing apps simpler and efficient.</span></span>

<span data-ttu-id="2803f-105">Hieronder volgen enkele van de uitbreidingen voor Azure AD in de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2803f-105">Following are some of the enhancements for Azure AD in the [Azure portal](https://portal.azure.com).</span></span>

- <span data-ttu-id="2803f-106">Een verbeterde toepassingsgalerie ervaring, met een vereenvoudigde toepassingsmodel maken en ondersteuning voor alle soorten toepassingen waarmee u bent.</span><span class="sxs-lookup"><span data-stu-id="2803f-106">An improved application gallery experience, with a simplified application creation model and support for all the application types that you’re used to.</span></span> 
- <span data-ttu-id="2803f-107">Een ervaring gloednieuw snel starten waarmee u kunt aan de slag met een test van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="2803f-107">A brand-new quick start experience that can help you get going with a pilot of your application.</span></span> 
- <span data-ttu-id="2803f-108">Selfservice-beleid configureren met een paar klikken.</span><span class="sxs-lookup"><span data-stu-id="2803f-108">Configure self-service policies with just a few clicks.</span></span> 
- <span data-ttu-id="2803f-109">Verbeteringen aan toepassingsproxy, eenmalige aanmelding configureren en breng uw eigen toepassingen mogelijk, zodat u meer gedaan dan voordat ophalen.</span><span class="sxs-lookup"><span data-stu-id="2803f-109">Improvements to application proxy, single sign-on configuration, and bring your own application experiences, allowing you to get more done than before.</span></span>

## <a name="improvements-to-the-azure-active-directory-application-gallery"></a><span data-ttu-id="2803f-110">Verbeteringen in de Azure Active Directory-Toepassingsgalerie</span><span class="sxs-lookup"><span data-stu-id="2803f-110">Improvements to the Azure Active Directory Application Gallery</span></span>

<span data-ttu-id="2803f-111">Toevoegen van uw favoriete toepassingen ongeacht of deze uit de [toepassingsgalerie](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery), aangepaste toepassingen die u wilt uitbreiden naar de cloud of nieuwe toepassingen die u ontwikkelt.</span><span class="sxs-lookup"><span data-stu-id="2803f-111">Add your favorite applications whether they are from the [application gallery](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery), custom applications you’re extending to the cloud, or new applications you’re developing.</span></span>  <span data-ttu-id="2803f-112">U kunt aan de slag met deze nieuwe ervaring door te klikken op **toevoegen** op de **bedrijfstoepassingen** overzicht of **alle toepassingen** blades.</span><span class="sxs-lookup"><span data-stu-id="2803f-112">You can get started with this new experience by clicking **Add** on the **Enterprise Applications** overview or **All applications** blades.</span></span>
 
  ![Een toepassing toevoegen](./media/active-directory-enterprise-apps-whats-new-azure-portal/01.png)

<span data-ttu-id="2803f-114">Eenmaal in de galerie ziet u onze uitgelichte toepassingen die ondersteuning bieden voor gebruikers inrichten begin-en-midden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="2803f-114">Once in the gallery, you’ll see all our featured applications which support user provisioning displayed front-and-center.</span></span>  <span data-ttu-id="2803f-115">Kunt u allerlei verschillende categorieën om de toepassingen die u interesseren inzoomen bladeren of kunt u de zoekfunctie snel vinden de toepassingen die u wilt integreren.</span><span class="sxs-lookup"><span data-stu-id="2803f-115">You can browse all sorts of different categories to drill into the applications you care about, or you can use the search experience to rapidly find the applications you want to integrate.</span></span>

  ![De galerie met toepassingen](./media/active-directory-enterprise-apps-whats-new-azure-portal/02.png)

## <a name="add-custom-applications-from-one-place"></a><span data-ttu-id="2803f-117">Toevoegen van aangepaste toepassingen vanaf één locatie</span><span class="sxs-lookup"><span data-stu-id="2803f-117">Add custom applications from one place</span></span>

<span data-ttu-id="2803f-118">Naast het toevoegen van vooraf geïntegreerde toepassingen uit de galerie, zijn configuratie van de aangepaste toepassing ondervindt dat u werden gebruikt in de klassieke beheerportal nu mogelijk in de nieuwe portal.</span><span class="sxs-lookup"><span data-stu-id="2803f-118">In addition to adding pre-integrated applications from the gallery, all the custom application configuration experiences that you were used to in the classic management portal are now possible in the new portal.</span></span> <span data-ttu-id="2803f-119">Of u een toepassing met on-premises met de toepassingsproxy integreren van uw eigen wachtwoord of de federatieve SSO-toepassing, uitbreiden of een gloednieuw toepassing met het toepassingsregister maakt, hebt u deze via deze één enkele locatie.</span><span class="sxs-lookup"><span data-stu-id="2803f-119">Whether you are extending an application from on-premises using the application proxy, integrating your own password or federated SSO application, or creating a brand-new application using the application registry, you can get to it all from this one single place.</span></span>

  ![Uw eigen toepassing toe te voegen](./media/active-directory-enterprise-apps-whats-new-azure-portal/03.png)

 
<span data-ttu-id="2803f-121">**Uw eigen toepassing toe te voegen aan de slag**:</span><span class="sxs-lookup"><span data-stu-id="2803f-121">**To get started adding your own application**:</span></span>

1. <span data-ttu-id="2803f-122">Klik op de **uw eigen koppeling toevoegen** boven aan de galerie met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="2803f-122">Click the **add your own link** at the top of the application gallery.</span></span> 
2. <span data-ttu-id="2803f-123">Ziet u twee opties voor u: **implementeren van een bestaande toepassing** of **ontwikkelen van een nieuwe toepassing**.</span><span class="sxs-lookup"><span data-stu-id="2803f-123">You’ll see two options in front of you: **deploy an existing application** or **develop a new application**.</span></span> <span data-ttu-id="2803f-124">Lees verder voor meer informatie over het verschil tussen de twee opties en hoe ze te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2803f-124">Read on to learn the difference between the two options and how to use them.</span></span>

### <a name="deploying-existing-applications"></a><span data-ttu-id="2803f-125">Bestaande toepassingen implementeren</span><span class="sxs-lookup"><span data-stu-id="2803f-125">Deploying existing applications</span></span>

1. <span data-ttu-id="2803f-126">Als u hebt een toepassing die al wordt uitgevoerd en alleen wilt integreren met Azure AD voor eenmalige aanmelding op of inrichting, kies de **implementeren van een bestaande toepassing** optie.</span><span class="sxs-lookup"><span data-stu-id="2803f-126">If you’ve got an application running already and just want to integrate it into Azure AD for single-sign on or provisioning, choose the **Deploy an existing application** option.</span></span> <span data-ttu-id="2803f-127">Kies een naam voor uw toepassing, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="2803f-127">Pick a name for your application, click **Add**.</span></span>
2. <span data-ttu-id="2803f-128">Dat is alles.</span><span class="sxs-lookup"><span data-stu-id="2803f-128">That's it!</span></span> <span data-ttu-id="2803f-129">In plaats van dat de details over uw toepassing vooraf te kennen, kunt u nu instellen hoe uw nieuwe toepassing werkt door te navigeren in het menu links en de toepassing naar wens configureren op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="2803f-129">Instead of needing to know all the details about your application up front, you can now set up how your new application works by navigating through the left menu and configuring the application to your liking at any time.</span></span>

  ![Toevoegen van een bestaande toepassing met één klik](./media/active-directory-enterprise-apps-whats-new-azure-portal/04.png)
 
### <a name="developing-new-applications"></a><span data-ttu-id="2803f-131">Ontwikkelen van nieuwe toepassingen</span><span class="sxs-lookup"><span data-stu-id="2803f-131">Developing new applications</span></span>

1. <span data-ttu-id="2803f-132">Als u een nieuwe toepassing ontwikkelt, is er een eenvoudige manier voor u direct aan het register van de toepassing uit de galerie:</span><span class="sxs-lookup"><span data-stu-id="2803f-132">If you’re developing a new application, there's an easy way for you to get to the Application Registry right from the gallery:</span></span>
2. <span data-ttu-id="2803f-133">Klik op de **toevoegen aan uw eigen** optie uit de galerie met toepassingen, selecteer de **ontwikkelen van een bestaande toepassing** keuze en u ziet een snelle koppeling aan de toepassing toevoegen-ervaring.</span><span class="sxs-lookup"><span data-stu-id="2803f-133">Click on the **add your own** option from the Application Gallery, select the **develop an existing application** choice, and you’ll see a quick link right to the application add experience.</span></span>

  ![Een toepassing recentelijk ontwikkelde toe te voegen in een paar klikken](./media/active-directory-enterprise-apps-whats-new-azure-portal/05.png)


>[!NOTE]
><span data-ttu-id="2803f-135">Als u een toepassing met het register van de toepassing toevoegt, wordt deze weergegeven in de lijst met bedrijfstoepassingen waar u zult kunnen eenmalige aanmelding configureren en beheren van beleidsregels voor toegang voor uw nieuwe toepassing weergegeven.</span><span class="sxs-lookup"><span data-stu-id="2803f-135">Once you add an application using the Application Registry, you’ll see it show up in the list of Enterprise Applications where you’ll be able to configure single sign-on and manage access policies for your new application.</span></span>

  ![Het beheren van toegang tot uw nieuwe toepassing onder bedrijfstoepassingen](./media/active-directory-enterprise-apps-whats-new-azure-portal/06.png)


## <a name="quick-start-get-going-with-your-new-application-right-away"></a><span data-ttu-id="2803f-137">Snel aan de slag: aan de slag met uw nieuwe toepassing meteen</span><span class="sxs-lookup"><span data-stu-id="2803f-137">Quick start: Get going with your new application right away</span></span> 

<span data-ttu-id="2803f-138">Nadat u een toepassing, of zijn de vooraf geïntegreerde of uw eigen app hebt toegevoegd, er een op maat gemaakte Snel starten-ervaring om u snel fundering in de nieuwe ervaring van toepassingen gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2803f-138">After you’ve added an application, whether it be pre-integrated or your own app, we’ve created a tailored quick-start experience to get you grounded in the new applications experience quickly.</span></span> <span data-ttu-id="2803f-139">Als u elke optie systematischer volgt, we helpt u stapsgewijs door de gebruikersinterface en hoe u aan de slag met een test van uw nieuwe toepassing zo snel mogelijk.</span><span class="sxs-lookup"><span data-stu-id="2803f-139">If you follow each option systematically, we’ll walk you through the UI and show you how to get going with a pilot of your new application as quickly as possible.</span></span> 
 
  ![De nieuwe toepassingen die snelle start ervaring](./media/active-directory-enterprise-apps-whats-new-azure-portal/07.png)

 <span data-ttu-id="2803f-141">U kunt deze nieuwe ervaring voor snel starten op elk gewenst moment en voor elke toepassing, door te klikken op **snel starten** in het menu van de linkernavigatiebalk toepassing.</span><span class="sxs-lookup"><span data-stu-id="2803f-141">You can visit this new quick start experience at any time, and for any application, by clicking on **Quick start** from the application left navigation menu.</span></span>


## <a name="updated-application-proxy-configuration"></a><span data-ttu-id="2803f-142">Bijgewerkte toepassing proxyconfiguratie</span><span class="sxs-lookup"><span data-stu-id="2803f-142">Updated application proxy configuration</span></span>
<span data-ttu-id="2803f-143">Nu gaan we als een van de nieuwe toepassingen die u hebt toegevoegd in uw on-premises omgeving wordt uitgevoerd en u wilt integreren met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2803f-143">Now, let’s say one of the new applications you added is running in your on-premises environment and you want to integrate it with Azure AD.</span></span>  <span data-ttu-id="2803f-144">Een van de cool nieuwe dingen over de nieuwe ervaring voor de configuratie van toepassing in de nieuwe Azure AD portal is dat door het verdelen van de toepassing aanmelding-modus van de configuratie van de toepassing proxy kan nu eenvoudig worden blootgesteld wachtwoord SSO of federatieve toepassingen die worden uitgevoerd in uw bedrijfsnetwerk rechts in de cloud, zonder te hoeven maken van meerdere exemplaren van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="2803f-144">One of the cool new things about the new application configuration experience in the new Azure AD portal is that by splitting the application’s sign-on mode from its application proxy configuration, you can now easily expose password SSO or federated applications that are running in your corporate network right to the cloud, without having to create multiple instances of the application.</span></span>

<span data-ttu-id="2803f-145">Naast dit, kunt u nu ook configureren van de nieuwe toepassingen die u hebt toegevoegd voor gebruik met Azure AD-toepassingsproxy rechts van de nieuwe portal, met inbegrip van toepassingen die ondersteuning bieden voor systeemeigen Windows-verificatie-ervaring.</span><span class="sxs-lookup"><span data-stu-id="2803f-145">In addition to this, you can now also configure any of the new applications you’ve added for use with the Azure AD Application Proxy right from the new portal, including applications which support native Windows authentication experiences.</span></span>

  ![Configureren van een toepassing de optie van de aanmelding geïntegreerde Windows-verificatie te gebruiken](./media/active-directory-enterprise-apps-whats-new-azure-portal/08.png)
 

<span data-ttu-id="2803f-147">Om te beginnen met een systeemeigen Windows-verificatie toepassing configureren met de toepassingsproxy:</span><span class="sxs-lookup"><span data-stu-id="2803f-147">To get started configuring a native Windows authentication application with the Application Proxy:</span></span>
1. <span data-ttu-id="2803f-148">Klik op het één aanmelding navigatie-item en kies **geïntegreerde Windows-verificatie** op de instellingenblade voor eenmalige aanmelding en de instellingen naar wens configureren.</span><span class="sxs-lookup"><span data-stu-id="2803f-148">Click on the Single sign-on navigation item and choose **Integrated Windows Authentication** from the sign-on settings blade and configure the settings to your liking.</span></span>
2. <span data-ttu-id="2803f-149">Boven op deze nieuwe verificatiemodi ondersteunen, kunt u certificaten van aangepaste domeinen om toepassingen die worden uitgevoerd op de beveiligde eindpunten binnen uw organisatie te ondersteunen nu ook uploaden.</span><span class="sxs-lookup"><span data-stu-id="2803f-149">On top of supporting these new authentication modes, you can now also upload certificates from custom domains to support applications running on secure endpoints within your organization.</span></span>  
 
   ![Uploaden van een certificaat moet worden gebruikt bij de toepassingsproxy](./media/active-directory-enterprise-apps-whats-new-azure-portal/09.png)

3. <span data-ttu-id="2803f-151">Als u wilt uploaden een nieuw certificaat voor uw favoriete on-premises toepassing, klikt u op de **toepassingsproxy** optie in het linkernavigatievenster menu, klikt u op de **certificaat** selector en upload een certificaat we gebruiken kunnen voor het versleutelen van uw toepassing aanvragen van onze cloudeindpunt-bestand.</span><span class="sxs-lookup"><span data-stu-id="2803f-151">To upload a new certificate for your favorite on-premises application, click on the **Application proxy** option from the left navigation menu, click the **Certificate** selector, and upload a certificate file we can use to encrypt requests from our cloud endpoint to your application.</span></span>

## <a name="advanced-federated-single-sign-on-configuration"></a><span data-ttu-id="2803f-152">Geavanceerde federatieve eenmalige aanmelding-configuratie</span><span class="sxs-lookup"><span data-stu-id="2803f-152">Advanced federated single sign-on configuration</span></span>

<span data-ttu-id="2803f-153">Voor de federatieve toepassingen vandaag gebruikt, moet u er veel nieuwe functies zijn in de aanmelding configuratie op basis van SAML-blade.</span><span class="sxs-lookup"><span data-stu-id="2803f-153">For those of you using federated applications today, there are many new features in the SAML-based sign-on configuration blade.</span></span> <span data-ttu-id="2803f-154">Beginnen met, kunt nu u volledig aanpassen, toevoegen, verwijderen en toewijzen van de bestaande gebruikerskenmerken als claims in SAML-tokens uitgegeven.</span><span class="sxs-lookup"><span data-stu-id="2803f-154">To start with, now you can fully customize, add, remove, and map the existing user attributes issued as claims in SAML tokens.</span></span>
 
  ![Aanpassen van de kenmerken van de SAML-token gebruiker doorgegeven aan een federatieve toepassing](./media/active-directory-enterprise-apps-whats-new-azure-portal/10.png)


<span data-ttu-id="2803f-156">Om te controleren dat uit de nieuwe federatieve SSO-configuratie:</span><span class="sxs-lookup"><span data-stu-id="2803f-156">To check that out the new federated SSO configuration:</span></span>
1. <span data-ttu-id="2803f-157">Open een federatieve toepassing **eenmalige aanmelding** blade in het linkernavigatievenster menu en zorg ervoor dat de '*op basis van SAML aanmelding** modus is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="2803f-157">Open a federated application’s **single sign-on** blade from the left navigation menu and make sure the ‘*SAML-based Sign-on** mode is selected.</span></span> 
2. <span data-ttu-id="2803f-158">Eenmaal er, schakel het selectievakje onder de **gebruikerskenmerken** kop wijzigen alle kenmerken die zijn opgenomen in het SAML-token wordt doorgegeven aan die toepassing.</span><span class="sxs-lookup"><span data-stu-id="2803f-158">Once there, enable the checkbox under the **User Attributes** heading to modify all of the attributes included in the SAML token passed to that application.</span></span>

<span data-ttu-id="2803f-159">U kunt ook maakt, rollover, en het beheren van certificaten gebruikt voor federatieve eenmalige aanmelding, evenals bewerken die met deze eigenschap wordt een melding wanneer uw certificaat is verlopen.</span><span class="sxs-lookup"><span data-stu-id="2803f-159">You can also create, rollover, and manage certificates used for federated single sign-on, as well as edit who gets notified when your certificate is about to expire.</span></span> <span data-ttu-id="2803f-160">Ziet u deze nieuwe opties onder de **certificaten** kop op de dezelfde eenmalige aanmelding blade.</span><span class="sxs-lookup"><span data-stu-id="2803f-160">You’ll see these new options under the **Certificates** heading on the same Single sign-on blade.</span></span>
 
  ![Maken van een nieuw certificaat verlopen meldingse-mail en opties voor Certificaatondertekening aanpassen](./media/active-directory-enterprise-apps-whats-new-azure-portal/11.png)

### <a name="relay-state-paramenter"></a><span data-ttu-id="2803f-162">Status van de relay-parameter worden</span><span class="sxs-lookup"><span data-stu-id="2803f-162">Relay State paramenter</span></span>
<span data-ttu-id="2803f-163">Ten slotte wordt ook de set parameters van SAML-URL wordt ondersteund als u wilt opnemen hebt uitgebreid de **parameter Relay State**, dit is de pagina die uw gebruikers terechtkomt op binnen een federatieve toepassing zodra de aanmeldingspagina is voltooid.</span><span class="sxs-lookup"><span data-stu-id="2803f-163">Finally, we’ve also extended the set of SAML URL parameters we support to include the **Relay State parameter**, which is the page your users will land on inside of a federated application once the sign-in is completed.</span></span> <span data-ttu-id="2803f-164">Dit is zeer nuttig instelling configureren als u wilt uw gebruikers verzenden met een specifieke locatie binnen de toepassing snel gaan ophalen.</span><span class="sxs-lookup"><span data-stu-id="2803f-164">This is very useful setting to configure if you want to send your users to a specific place within the application to get them going quickly.</span></span>

  ![Als u de status van SAML-Relay-parameter](./media/active-directory-enterprise-apps-whats-new-azure-portal/12.png)
 
<span data-ttu-id="2803f-166">**Instellen van de relay-parameter state**:</span><span class="sxs-lookup"><span data-stu-id="2803f-166">**To set the relay state parameter**:</span></span>

1. <span data-ttu-id="2803f-167">Inschakelen de **weergeven geavanceerde instellingen voor URL** selectievakje onder de **domein en de URL's** kop op eenmalige aanmelding op de blade configuratie.</span><span class="sxs-lookup"><span data-stu-id="2803f-167">Enable the **Show advanced URL settings** check-box under the **Domain and URLs** heading on the single-sign on configuration blade.</span></span> 
2. <span data-ttu-id="2803f-168">Wanneer u dit doet, ziet u dat een set nieuwe URL invoer vakken weergegeven waarmee u kunt deze en andere, instellingen voor SAML-URL ingesteld.</span><span class="sxs-lookup"><span data-stu-id="2803f-168">Once you do this, you’ll see a set of new URL input boxes appear which will allow you to set this, and other, SAML URL settings.</span></span>

## <a name="bring-your-own-password-sso-applications"></a><span data-ttu-id="2803f-169">Breng uw eigen wachtwoord SSO-toepassingen</span><span class="sxs-lookup"><span data-stu-id="2803f-169">Bring your own password SSO applications</span></span>

<span data-ttu-id="2803f-170">We weten dat niet elke toepassing federation klare ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="2803f-170">We know that not every application supports federation right out of the box.</span></span> <span data-ttu-id="2803f-171">Zo mogelijk heeft een van de nieuwe toepassingen die u hebt toegevoegd een aangepast aanmeldingsscherm die uw gebruikers gebruiken een gebruikersnaam en wachtwoord aanmelden bij.</span><span class="sxs-lookup"><span data-stu-id="2803f-171">For example, maybe one of the new applications you added has a custom login screen that your users use a username and password to sign in to.</span></span> <span data-ttu-id="2803f-172">U kunt nog steeds deze soorten toepassingen integreren met Azure AD via onze **brengt uw eigen toepassingen** functie is nu beschikbaar voor u in de nieuwe portal te configureren.</span><span class="sxs-lookup"><span data-stu-id="2803f-172">You can still integrate these types of applications with Azure AD using our **Bring your own applications** feature, which is now available for you to configure in the new portal.</span></span>
 
  ![Integratie van aangepaste wachtwoord vaulting toepassingen met Azure AD](./media/active-directory-enterprise-apps-whats-new-azure-portal/13.png)

<span data-ttu-id="2803f-174">**De functie 'Brengt uw eigen toepassingen' uitchecken**:</span><span class="sxs-lookup"><span data-stu-id="2803f-174">**To check out the 'Bring your own applications' feature**:</span></span>

1. <span data-ttu-id="2803f-175">Na het instellen van de modus voor één aanmelding voor een nieuwe aangepaste toepassing die u hebt toegevoegd aan **op basis van wachtwoorden aanmelding**, voert u de URL waar de toepassing de aanmeldingsscherm renders en klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="2803f-175">After you set the single sign-on mode for a new custom application that you’ve added to **Password-based Sign-on**, enter the URL where the application renders its login screen and click **Save**.</span></span>  
2. <span data-ttu-id="2803f-176">Zodra u dat doet, wordt je automatisch scrape die URL voor een gebruikersnaam en wachtwoord invoervak en kunt u Azure AD gebruiken voor het veilig verzenden van wachtwoorden voor deze toepassing met behulp van de uitbreiding voor toegang tot Configuratiescherm browser.</span><span class="sxs-lookup"><span data-stu-id="2803f-176">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you to use Azure AD to securely transmit passwords to that application using the access panel browser extension.</span></span>

## <a name="configure-self-service-application-access"></a><span data-ttu-id="2803f-177">Toegang tot selfservice-toepassingen configureren</span><span class="sxs-lookup"><span data-stu-id="2803f-177">Configure self-service application access</span></span>

<span data-ttu-id="2803f-178">Nadat u veel nieuwe toepassingen hebt toegevoegd, mogelijk wilt u uw gebruikers om te bladeren en deze toepassingen aan hun eigen deelvensters toegang toevoegen zonder zin hebt u als beheerder in staat.</span><span class="sxs-lookup"><span data-stu-id="2803f-178">After you’ve added lots of new applications, maybe you want to allow your users to browse and add those applications to their own access panels, without needing to bother you as an administrator.</span></span> <span data-ttu-id="2803f-179">U kunt in deze nieuwe versie nu configureren en beheren van toegang tot selfservice toepassingen rechtstreeks vanuit de nieuwe portal.</span><span class="sxs-lookup"><span data-stu-id="2803f-179">Now, with this latest release, you can configure and manage self-service application access right from the new portal.</span></span>

  ![Toegang tot de toepassing zelf om een wachtwoord SSO-toepassing configureren](./media/active-directory-enterprise-apps-whats-new-azure-portal/14.png)
 
<span data-ttu-id="2803f-181">**Configureren en beheren van toegang tot de toepassing zelf**:</span><span class="sxs-lookup"><span data-stu-id="2803f-181">**To configure and manage self-service application access**:</span></span>

1. <span data-ttu-id="2803f-182">Om te beginnen, kunt u de **Self-service** optie van de toepassing navigatiemenu links en instellen van de **toestaan dat gebruikers toegang tot deze toepassing aanvragen?** optie naar '**Ja**'.</span><span class="sxs-lookup"><span data-stu-id="2803f-182">To get started, you can select the **Self-service** option from the application’s left navigation menu and set the **Allow users to request access to this application?** option to ‘**Yes**’.</span></span> 
2. <span data-ttu-id="2803f-183">Hierdoor kunt u configureren die is toegestaan voor het goedkeuren van toegang tot deze toepassing, en welke groep Self-Service gebruikers worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="2803f-183">This will enable you to configure who is allowed to approve access to this application, and which group self-service users will be added.</span></span> <span data-ttu-id="2803f-184">Bovendien, als de toepassing is geconfigureerd voor wachtwoord eenmalige aanmelding, ziet ook u een andere optie waarmee u toestaan die goedkeurders voor het beheren van de wachtwoorden die zijn toegewezen aan de toepassing.</span><span class="sxs-lookup"><span data-stu-id="2803f-184">In addition, if the application is configured for password single-sign on, you’ll also see another option which lets you optionally allow those approvers to manage the passwords assigned to the application.</span></span>

##<a name="feedback"></a><span data-ttu-id="2803f-185">Feedback</span><span class="sxs-lookup"><span data-stu-id="2803f-185">Feedback</span></span>

<span data-ttu-id="2803f-186">We hopen dat u u zoals het gebruik van het verbeterde ervaring voor Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2803f-186">We hope you like using the improved Azure AD experience.</span></span> <span data-ttu-id="2803f-187">Zorg ervoor dat uw feedback!</span><span class="sxs-lookup"><span data-stu-id="2803f-187">Please keep the feedback coming!</span></span> <span data-ttu-id="2803f-188">Plaats uw feedback en ideeën voor verbetering van de **beheerportal** sectie van onze [Feedbackforum](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal).</span><span class="sxs-lookup"><span data-stu-id="2803f-188">Post your feedback and ideas for improvement in the **Admin Portal** section of our [feedback forum](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal).</span></span>  <span data-ttu-id="2803f-189">We enthousiast bent over het bouwen van cool nieuw per dag uit, en gebruik de richtlijnen voor vorm en definiëren wat we hierna bouwen.</span><span class="sxs-lookup"><span data-stu-id="2803f-189">We’re excited about building cool new stuff every day, and use your guidance to shape and define what we build next.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2803f-190">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2803f-190">Next steps</span></span>

<span data-ttu-id="2803f-191">Zie voor meer informatie [toepassingen beheren met Azure Active Directory](active-directory-enable-sso-scenario.md).</span><span class="sxs-lookup"><span data-stu-id="2803f-191">For more details, see [Managing Applications with Azure Active Directory](active-directory-enable-sso-scenario.md).</span></span>



