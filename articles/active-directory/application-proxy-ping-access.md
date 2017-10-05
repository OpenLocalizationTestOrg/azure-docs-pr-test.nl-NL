---
title: Verificatie op basis van een header met PingAccess voor Azure AD-toepassingsproxy | Microsoft Docs
description: Toepassingen publiceren met PingAccess en App-Proxy naar header gebaseerde verificatie ondersteunt.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 58034ab8830cf655199875b448948ea14dc04a70
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="header-based-authentication-for-single-sign-on-with-application-proxy-and-pingaccess"></a><span data-ttu-id="a7c05-103">Verificatie op basis van een koptekst voor eenmalige aanmelding met toepassingsproxy en PingAccess</span><span class="sxs-lookup"><span data-stu-id="a7c05-103">Header-based authentication for single sign-on with Application Proxy and PingAccess</span></span>

<span data-ttu-id="a7c05-104">Azure Active Directory-toepassingsproxy en PingAccess hebben hun samen Azure Active Directory om klanten te bieden met toegang tot zelfs meer toepassingen.</span><span class="sxs-lookup"><span data-stu-id="a7c05-104">Azure Active Directory Application Proxy and PingAccess have partnered together to provide Azure Active Directory customers with access to even more applications.</span></span> <span data-ttu-id="a7c05-105">PingAccess breidt de [bestaande toepassingsproxy aanbiedingen](active-directory-application-proxy-get-started.md) om op te nemen van één aanmelding toegang tot toepassingen die gebruikmaken van headers voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="a7c05-105">PingAccess expands the [existing Application Proxy offerings](active-directory-application-proxy-get-started.md) to include single sign-on access to applications that use headers for authentication.</span></span>

## <a name="what-is-pingaccess-for-azure-ad"></a><span data-ttu-id="a7c05-106">Wat is PingAccess voor Azure AD?</span><span class="sxs-lookup"><span data-stu-id="a7c05-106">What is PingAccess for Azure AD?</span></span>

<span data-ttu-id="a7c05-107">PingAccess voor Azure Active Directory is een aanbieding van PingAccess waarmee u gebruikerstoegang en eenmalige aanmelding geven tot toepassingen die gebruikmaken van headers voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="a7c05-107">PingAccess for Azure Active Directory is an offering of PingAccess that enables you to give users access and single sign-on to applications that use headers for authentication.</span></span> <span data-ttu-id="a7c05-108">Een toepassing Proxy beschouwt deze apps zoals elke andere, met behulp van Azure AD verifiëren van toegang en vervolgens verkeer via de connector-service wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="a7c05-108">Application Proxy treats these apps like any other, using Azure AD to authenticate access and then passing traffic through the connector service.</span></span> <span data-ttu-id="a7c05-109">PingAccess bevindt zich voor de apps en zet het toegangstoken van Azure AD in een koptekst, zodat de toepassing de verificatie in de indeling die kan gelezen ontvangt.</span><span class="sxs-lookup"><span data-stu-id="a7c05-109">PingAccess sits in front of the apps and translates the access token from Azure AD into a header so that the application receives the authentication in the format it can read.</span></span>

<span data-ttu-id="a7c05-110">Uw gebruikers won't iets anders zien wanneer ze zich aanmelden voor gebruik van uw zakelijke apps.</span><span class="sxs-lookup"><span data-stu-id="a7c05-110">Your users won’t notice anything different when they sign in to use your corporate apps.</span></span> <span data-ttu-id="a7c05-111">Ze kunnen nog steeds overal werken uit op elk apparaat.</span><span class="sxs-lookup"><span data-stu-id="a7c05-111">They can still work from anywhere on any device.</span></span> 

<span data-ttu-id="a7c05-112">Aangezien de toepassingsproxy-connectors externe verkeer naar alle apps, ongeacht hun verificatietype omleiden, moeten ze blijven automatisch, maar ook voor taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="a7c05-112">Since the Application Proxy connectors direct remote traffic to all apps regardless of their authentication type, they’ll continue to load balance automatically, as well.</span></span>

## <a name="how-do-i-get-access"></a><span data-ttu-id="a7c05-113">Hoe krijg ik toegang?</span><span class="sxs-lookup"><span data-stu-id="a7c05-113">How do I get access?</span></span>

<span data-ttu-id="a7c05-114">Aangezien dit scenario wordt aangeboden via een samenwerking tussen Azure Active Directory en PingAccess, moet u licenties voor beide services.</span><span class="sxs-lookup"><span data-stu-id="a7c05-114">Since this scenario is offered through a partnership between Azure Active Directory and PingAccess, you need licenses for both services.</span></span> <span data-ttu-id="a7c05-115">Azure Active Directory Premium-abonnementen bevatten echter een PingAccess standaardlicentie die betrekking heeft op maximaal 20 toepassingen.</span><span class="sxs-lookup"><span data-stu-id="a7c05-115">However, Azure Active Directory Premium subscriptions include a basic PingAccess license that covers up to 20 applications.</span></span> <span data-ttu-id="a7c05-116">Als u moet u meer dan 20 headers gebaseerde toepassingen publiceert, kunt u een extra licentie aanschaffen bij PingAccess.</span><span class="sxs-lookup"><span data-stu-id="a7c05-116">If you need to publish more than 20 header-based applications, you can purchase an additional license from PingAccess.</span></span> 

<span data-ttu-id="a7c05-117">Zie [Azure Active Directory-edities](active-directory-editions.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a7c05-117">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

## <a name="publish-your-application-in-azure"></a><span data-ttu-id="a7c05-118">Uw toepassing publiceren in Azure</span><span class="sxs-lookup"><span data-stu-id="a7c05-118">Publish your application in Azure</span></span>

<span data-ttu-id="a7c05-119">In dit artikel is bedoeld voor personen die een app met dit scenario voor het eerst wilt publiceren.</span><span class="sxs-lookup"><span data-stu-id="a7c05-119">This article is intended for people who are publishing an app with this scenario for the first time.</span></span> <span data-ttu-id="a7c05-120">Dit helpt bij het aan de slag met de toepassings- en PingAccess, naast de publishing stappen.</span><span class="sxs-lookup"><span data-stu-id="a7c05-120">It walks through how to get started with both Application and PingAccess, in addition to the publishing steps.</span></span> <span data-ttu-id="a7c05-121">Als u beide services al hebt geconfigureerd, maar een refresher op de publicatie stappen wilt, kunt u de installatie van de connector overslaan en verplaatsen naar [uw app toevoegen aan Azure AD met toepassingsproxy](#add-your-app-to-Azure-AD-with-Application-Proxy).</span><span class="sxs-lookup"><span data-stu-id="a7c05-121">If you’ve already configured both services but want a refresher on the publishing steps, you can skip the connector installation and move on to [Add your app to Azure AD with Application Proxy](#add-your-app-to-Azure-AD-with-Application-Proxy).</span></span>

>[!NOTE]
><span data-ttu-id="a7c05-122">Omdat dit scenario een verbinding tussen Azure AD is en PingAccess, enkele van de instructies aanwezig zijn op de identiteit van de Ping-site.</span><span class="sxs-lookup"><span data-stu-id="a7c05-122">Since this scenario is a partnership between Azure AD and PingAccess, some of the instructions exist on the Ping Identity site.</span></span>

### <a name="install-an-application-proxy-connector"></a><span data-ttu-id="a7c05-123">Een Application Proxy connector installeren</span><span class="sxs-lookup"><span data-stu-id="a7c05-123">Install an Application Proxy connector</span></span>

<span data-ttu-id="a7c05-124">Als u al Application Proxy ingeschakeld hebt en hebt een connector is geïnstalleerd, kunt u deze sectie overslaan en verplaatst op naar [uw app toevoegen aan Azure AD met toepassingsproxy](#add-your-app-to-azure-ad-with-application-proxy).</span><span class="sxs-lookup"><span data-stu-id="a7c05-124">If you already have Application Proxy enabled, and have a connector installed, you can skip this section and move on to [Add your app to Azure AD with Application Proxy](#add-your-app-to-azure-ad-with-application-proxy).</span></span>

<span data-ttu-id="a7c05-125">De connector voor toepassingsproxy is een Windows Server-service die het verkeer van uw werknemers extern naar uw gepubliceerde apps wordt verwezen.</span><span class="sxs-lookup"><span data-stu-id="a7c05-125">The Application Proxy connector is a Windows Server service that directs the traffic from your remote employees to your published apps.</span></span> <span data-ttu-id="a7c05-126">Zie voor meer installatie-instructies, [toepassingsproxy inschakelen in de Azure portal](active-directory-application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="a7c05-126">For more detailed installation instructions, see [Enable Application Proxy in the Azure portal](active-directory-application-proxy-enable.md).</span></span>

1. <span data-ttu-id="a7c05-127">Aanmelden bij de [Azure-portal](https://portal.azure.com) als globale beheerder.</span><span class="sxs-lookup"><span data-stu-id="a7c05-127">Sign in to the [Azure portal](https://portal.azure.com) as a global administrator.</span></span>
2. <span data-ttu-id="a7c05-128">Selecteer **Azure Active Directory** > **toepassingsproxy**.</span><span class="sxs-lookup"><span data-stu-id="a7c05-128">Select **Azure Active Directory** > **Application proxy**.</span></span>
3. <span data-ttu-id="a7c05-129">Selecteer **Connector downloaden** om de Application Proxy connector downloaden te starten.</span><span class="sxs-lookup"><span data-stu-id="a7c05-129">Select **Download Connector** to start the Application Proxy connector download.</span></span> <span data-ttu-id="a7c05-130">Volg de installatie-instructies.</span><span class="sxs-lookup"><span data-stu-id="a7c05-130">Follow the installation instructions.</span></span>

   ![Toepassingsproxy inschakelen en de connector downloaden](./media/application-proxy-ping-access/install-connector.png)

4. <span data-ttu-id="a7c05-132">Downloaden van de connector moet automatisch toepassingsproxy inschakelen voor uw directory, maar als u dit niet kunt selecteren **Enable Application Proxy**.</span><span class="sxs-lookup"><span data-stu-id="a7c05-132">Downloading the connector should automatically enable Application Proxy for your directory, but if not you can select **Enable Application Proxy**.</span></span>


### <a name="add-your-app-to-azure-ad-with-application-proxy"></a><span data-ttu-id="a7c05-133">Uw app toevoegen aan Azure AD met toepassingsproxy</span><span class="sxs-lookup"><span data-stu-id="a7c05-133">Add your app to Azure AD with Application Proxy</span></span>

<span data-ttu-id="a7c05-134">Er zijn twee stappen die u moet nemen in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a7c05-134">There are two actions you need to take in the Azure portal.</span></span> <span data-ttu-id="a7c05-135">Eerst moet u uw toepassing met toepassingsproxy publiceren.</span><span class="sxs-lookup"><span data-stu-id="a7c05-135">First, you need to publish your application with Application Proxy.</span></span> <span data-ttu-id="a7c05-136">Vervolgens moet u voor het verzamelen van informatie over de app die u kunt tijdens de stappen PingAccess gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a7c05-136">Then, you need to collect some information about the app that you can use during the PingAccess steps.</span></span>

<span data-ttu-id="a7c05-137">Volg deze stappen voor het publiceren van uw app.</span><span class="sxs-lookup"><span data-stu-id="a7c05-137">Follow these steps to publish your app.</span></span> <span data-ttu-id="a7c05-138">Voor een meer overzicht van de stappen 1-8, Zie gedetailleerde [toepassingen publiceren met Azure AD-toepassingsproxy](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a7c05-138">For a more detailed walkthrough of steps 1-8, see [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

1. <span data-ttu-id="a7c05-139">Als dat niet in de laatste sectie aanmelden bij de [Azure-portal](https://portal.azure.com) als globale beheerder.</span><span class="sxs-lookup"><span data-stu-id="a7c05-139">If you didn't in the last section, sign in to the [Azure portal](https://portal.azure.com) as a global administrator.</span></span>
2. <span data-ttu-id="a7c05-140">Selecteer **Azure Active Directory** > **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="a7c05-140">Select **Azure Active Directory** > **Enterprise applications**.</span></span>
3. <span data-ttu-id="a7c05-141">Selecteer **toevoegen** boven aan de blade.</span><span class="sxs-lookup"><span data-stu-id="a7c05-141">Select **Add** at the top of the blade.</span></span>
4. <span data-ttu-id="a7c05-142">Selecteer **On-premises toepassing**.</span><span class="sxs-lookup"><span data-stu-id="a7c05-142">Select **On-premises application**.</span></span>
5. <span data-ttu-id="a7c05-143">Vul de vereiste velden met informatie over uw nieuwe app.</span><span class="sxs-lookup"><span data-stu-id="a7c05-143">Fill out the required fields with information about your new app.</span></span> <span data-ttu-id="a7c05-144">Gebruik de volgende richtlijnen voor de instellingen:</span><span class="sxs-lookup"><span data-stu-id="a7c05-144">Use the following guidance for the settings:</span></span>
   - <span data-ttu-id="a7c05-145">**Interne URL**: normaal bieden u de URL die u u naar de aanmeldingspagina van de app gaat als u op het bedrijfsnetwerk bevinden.</span><span class="sxs-lookup"><span data-stu-id="a7c05-145">**Internal URL**: Normally you provide the URL that takes you to the app’s sign in page when you’re on the corporate network.</span></span> <span data-ttu-id="a7c05-146">Voor dit scenario moet de connector de proxy PingAccess behandelen als de voorpagina van de app.</span><span class="sxs-lookup"><span data-stu-id="a7c05-146">For this scenario the connector needs to treat the PingAccess proxy as the front page of the app.</span></span> <span data-ttu-id="a7c05-147">Gebruik de volgende notatie: `https://<host name of your PA server>:<port>`.</span><span class="sxs-lookup"><span data-stu-id="a7c05-147">Use this format: `https://<host name of your PA server>:<port>`.</span></span> <span data-ttu-id="a7c05-148">De poort is 3000 standaard, maar u kunt deze configureren in PingAccess.</span><span class="sxs-lookup"><span data-stu-id="a7c05-148">The port is 3000 by default, but you can configure it in PingAccess.</span></span>
   - <span data-ttu-id="a7c05-149">**Methode voor verificatie vooraf**: Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a7c05-149">**Pre-authentication method**: Azure Active Directory</span></span>
   - <span data-ttu-id="a7c05-150">**URL in de Headers vertalen**: Nee</span><span class="sxs-lookup"><span data-stu-id="a7c05-150">**Translate URL in Headers**: No</span></span>

   >[!NOTE]
   ><span data-ttu-id="a7c05-151">Als dit uw eerste toepassing, moet u poort 3000 gebruiken om te starten en keert u terug naar het bijwerken van deze instelling als u de configuratie van uw PingAccess wijzigt.</span><span class="sxs-lookup"><span data-stu-id="a7c05-151">If this is your first application, use port 3000 to start and come back to update this setting if you change your PingAccess configuration.</span></span> <span data-ttu-id="a7c05-152">Als dit uw app tweede of hoger, moet dit overeen met de Listener die u hebt geconfigureerd in PingAccess.</span><span class="sxs-lookup"><span data-stu-id="a7c05-152">If this is your second or later app, this will need to match the Listener you’ve configured in PingAccess.</span></span> <span data-ttu-id="a7c05-153">Meer informatie over [luisteraars in PingAccess](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html).</span><span class="sxs-lookup"><span data-stu-id="a7c05-153">Learn more about [listeners in PingAccess](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html).</span></span>

6. <span data-ttu-id="a7c05-154">Selecteer **toevoegen** onderaan de blade.</span><span class="sxs-lookup"><span data-stu-id="a7c05-154">Select **Add** at the bottom of the blade.</span></span> <span data-ttu-id="a7c05-155">Uw toepassing wordt toegevoegd en het menu Snel starten wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="a7c05-155">Your application is added, and the quick start menu opens.</span></span>
7. <span data-ttu-id="a7c05-156">Selecteer in het menu Snel starten **een gebruiker toewijzen voor het testen van**, en ten minste één gebruiker toevoegen aan de toepassing.</span><span class="sxs-lookup"><span data-stu-id="a7c05-156">In the quick start menu, select **Assign a user for testing**, and add at least one user to the application.</span></span> <span data-ttu-id="a7c05-157">Zorg ervoor dat deze testaccount toegang heeft tot de on-premises toepassing.</span><span class="sxs-lookup"><span data-stu-id="a7c05-157">Make sure this test account has access to the on-premises application.</span></span>
8. <span data-ttu-id="a7c05-158">Selecteer **toewijzen** om op te slaan van de toewijzing van de gebruiker test.</span><span class="sxs-lookup"><span data-stu-id="a7c05-158">Select **Assign** to save the test user assignment.</span></span>
9. <span data-ttu-id="a7c05-159">Selecteer op de blade app management **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="a7c05-159">On the app management blade, select **Single sign-on**.</span></span>
10. <span data-ttu-id="a7c05-160">Kies **headers gebaseerde aanmelding** uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="a7c05-160">Choose **Header-based sign-on** from the drop-down menu.</span></span> <span data-ttu-id="a7c05-161">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a7c05-161">Select **Save**.</span></span>

   >[!TIP]
   ><span data-ttu-id="a7c05-162">Als dit de eerste keer is op basis van een koptekst eenmalige aanmelding, moet u PingAccess installeren.</span><span class="sxs-lookup"><span data-stu-id="a7c05-162">If this is your first time using header-based single sign-on, you need to install PingAccess.</span></span> <span data-ttu-id="a7c05-163">Gebruik de koppeling om te zorgen dat uw Azure-abonnement is automatisch gekoppeld aan uw installatie PingAccess, in op deze pagina voor eenmalige aanmelding PingAccess downloaden.</span><span class="sxs-lookup"><span data-stu-id="a7c05-163">To make sure your Azure subscription is automatically associated with your PingAccess installation, use the link on this single sign-on page to download PingAccess.</span></span> <span data-ttu-id="a7c05-164">U kunt nu de downloadsite openen of naar deze pagina later terugkomen.</span><span class="sxs-lookup"><span data-stu-id="a7c05-164">You can open the download site now, or come back to this page later.</span></span> 

   ![Selecteer op basis van een koptekst eenmalige aanmelding](./media/application-proxy-ping-access/sso-header.PNG)

11. <span data-ttu-id="a7c05-166">Sluit de blade van Enterprise-toepassingen of schuif helemaal naar links om te keren naar het menu van Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a7c05-166">Close the Enterprise applications blade or scroll all the way to the left to return to the Azure Active Directory menu.</span></span>
12. <span data-ttu-id="a7c05-167">Selecteer **App registraties**.</span><span class="sxs-lookup"><span data-stu-id="a7c05-167">Select **App registrations**.</span></span>

   ![Selecteer de App-registraties](./media/application-proxy-ping-access/app-registrations.png)

13. <span data-ttu-id="a7c05-169">Selecteer de app die u zojuist hebt toegevoegd, klikt u vervolgens **antwoord-URL's**.</span><span class="sxs-lookup"><span data-stu-id="a7c05-169">Select the app you just added, then **Reply URLs**.</span></span>

   ![Selecteer de antwoord-URL 's](./media/application-proxy-ping-access/reply-urls.png)

14. <span data-ttu-id="a7c05-171">Controleer de externe URL die u hebt toegewezen aan uw app in stap 5 is als in de lijst antwoord-URL's.</span><span class="sxs-lookup"><span data-stu-id="a7c05-171">Check to see if the external URL that you assigned to your app in step 5 is in the Reply URLs list.</span></span> <span data-ttu-id="a7c05-172">Als dit niet het geval is, moet u deze nu toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a7c05-172">If it’s not, add it now.</span></span>
15. <span data-ttu-id="a7c05-173">Selecteer op het tabblad app-instellingen **vereist machtigingen**.</span><span class="sxs-lookup"><span data-stu-id="a7c05-173">On the app settings blade, select **Required permissions**.</span></span>

  ![Selecteer de vereiste machtigingen](./media/application-proxy-ping-access/required-permissions.png)

16. <span data-ttu-id="a7c05-175">Selecteer **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="a7c05-175">Select **Add**.</span></span> <span data-ttu-id="a7c05-176">Kies voor de API **Windows Azure Active Directory**, klikt u vervolgens **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="a7c05-176">For the API, choose **Windows Azure Active Directory**, then **Select**.</span></span> <span data-ttu-id="a7c05-177">Voor de machtigingen kiest **lezen en schrijven van alle toepassingen** en **aanmelden en gebruikersprofiel lezen**, vervolgens **Selecteer** en **gedaan**.</span><span class="sxs-lookup"><span data-stu-id="a7c05-177">For the permissions, choose **Read and write all applications** and **Sign in and read user profile**, then **Select** and **Done**.</span></span>  

  ![Selecteer machtigingen](./media/application-proxy-ping-access/select-permissions.png)

### <a name="collect-information-for-the-pingaccess-steps"></a><span data-ttu-id="a7c05-179">Informatie voor de stappen PingAccess verzamelen</span><span class="sxs-lookup"><span data-stu-id="a7c05-179">Collect information for the PingAccess steps</span></span>

1. <span data-ttu-id="a7c05-180">Selecteer op de blade van uw app-instellingen **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="a7c05-180">On your app settings blade, select **Properties**.</span></span> 

  ![Eigenschappen selecteren](./media/application-proxy-ping-access/properties.png)

2. <span data-ttu-id="a7c05-182">Sla de **toepassings-Id** waarde.</span><span class="sxs-lookup"><span data-stu-id="a7c05-182">Save the **Application Id** value.</span></span> <span data-ttu-id="a7c05-183">Dit wordt gebruikt voor de client-ID wanneer u PingAccess configureert.</span><span class="sxs-lookup"><span data-stu-id="a7c05-183">This is used for the client ID when you configure PingAccess.</span></span>
3. <span data-ttu-id="a7c05-184">Selecteer op het tabblad app-instellingen **sleutels**.</span><span class="sxs-lookup"><span data-stu-id="a7c05-184">On the app settings blade, select **Keys**.</span></span>

  ![Selecteer sleutels](./media/application-proxy-ping-access/Keys.png)

4. <span data-ttu-id="a7c05-186">Een sleutel maken door te voeren van een sleutel beschrijving en een vervaldatum kiezen uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="a7c05-186">Create a key by entering a key description and choosing an expiration date from the drop-down menu.</span></span>
5. <span data-ttu-id="a7c05-187">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a7c05-187">Select **Save**.</span></span> <span data-ttu-id="a7c05-188">Een GUID die wordt weergegeven in de **waarde** veld.</span><span class="sxs-lookup"><span data-stu-id="a7c05-188">A GUID appears in the **Value** field.</span></span>

  <span data-ttu-id="a7c05-189">Deze waarde nu niet opslaan omdat het niet mogelijk om het te bekijken opnieuw nadat u dit venster sluiten.</span><span class="sxs-lookup"><span data-stu-id="a7c05-189">Save this value now, as you won’t be able to see it again after you close this window.</span></span>

  ![Maak een nieuwe sleutel](./media/application-proxy-ping-access/create-keys.png)

6. <span data-ttu-id="a7c05-191">Sluit de blade van App-registraties of schuif helemaal naar links om te keren naar het menu van Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a7c05-191">Close the App registrations blade or scroll all the way to the left to return to the Azure Active Directory menu.</span></span>
7. <span data-ttu-id="a7c05-192">Selecteer **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="a7c05-192">Select **Properties**.</span></span>
8. <span data-ttu-id="a7c05-193">Sla de **map-ID** GUID.</span><span class="sxs-lookup"><span data-stu-id="a7c05-193">Save the **Directory ID** GUID.</span></span>

### <a name="optional---update-graphapi-to-send-custom-fields"></a><span data-ttu-id="a7c05-194">Optioneel - Update GraphAPI voor het verzenden van aangepaste velden</span><span class="sxs-lookup"><span data-stu-id="a7c05-194">Optional - Update GraphAPI to send custom fields</span></span>

<span data-ttu-id="a7c05-195">Zie voor een lijst van beveiligingstokens die door Azure AD voor verificatie verzonden, [Azure AD-tokenverwijzing](./develop/active-directory-token-and-claims.md).</span><span class="sxs-lookup"><span data-stu-id="a7c05-195">For a list of security tokens that Azure AD sends for authentication, see [Azure AD token reference](./develop/active-directory-token-and-claims.md).</span></span> <span data-ttu-id="a7c05-196">Als u een aangepaste claim die door andere tokens verzonden moet, gebruikt u GraphAPI instellen van het veld app *acceptMappedClaims* naar **True**.</span><span class="sxs-lookup"><span data-stu-id="a7c05-196">If you need a custom claim that sends other tokens, use GraphAPI to set the app field *acceptMappedClaims* to **True**.</span></span> <span data-ttu-id="a7c05-197">U kunt Azure AD Graph Explorer of MS Graph gebruiken om deze configuratie.</span><span class="sxs-lookup"><span data-stu-id="a7c05-197">You can use either Azure AD Graph Explorer or MS Graph to make this configuration.</span></span> 

<span data-ttu-id="a7c05-198">In dit voorbeeld wordt een grafiek Explorer:</span><span class="sxs-lookup"><span data-stu-id="a7c05-198">This example uses Graph Explorer:</span></span>

```
PATCH https://graph.windows.net/myorganization/applications/<object_id_GUID_of_your_application> 

{
  "acceptMappedClaims":true
}
```

## <a name="download-pingaccess-and-configure-your-app"></a><span data-ttu-id="a7c05-199">PingAccess downloaden en configureren van uw app</span><span class="sxs-lookup"><span data-stu-id="a7c05-199">Download PingAccess and configure your app</span></span>

<span data-ttu-id="a7c05-200">Nu dat u de stappen voor de installatie Azure Active Directory hebt voltooid, kunt u met het configureren van PingAccess op verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="a7c05-200">Now that you've completed all the Azure Active Directory setup steps, you can move on to configuring PingAccess.</span></span> 

<span data-ttu-id="a7c05-201">De gedetailleerde stappen voor het PingAccess deel uitmaken van dit scenario blijven in de documentatie van de identiteit van de Ping [PingAccess configureren voor Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html).</span><span class="sxs-lookup"><span data-stu-id="a7c05-201">The detailed steps for the PingAccess part of this scenario continue in the Ping Identity documentation, [Configure PingAccess for Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html).</span></span>

<span data-ttu-id="a7c05-202">Deze stappen maakt u het proces van het ophalen van een account PingAccess als u er nog geen hebt, de PingAccess-Server installeren en een Azure AD OIDC providerverbinding maken met de ID van de Directory die u hebt gekopieerd uit de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a7c05-202">Those steps walk you through the process of getting a PingAccess account if you don't already have one, installing the PingAccess Server, and creating an Azure AD OIDC Provider connection with the Directory ID that you copied from the Azure portal.</span></span> <span data-ttu-id="a7c05-203">Vervolgens gebruikt u de waarden toepassings-ID en sleutel voor het maken van een websessie op PingAccess.</span><span class="sxs-lookup"><span data-stu-id="a7c05-203">Then, you use the Application ID and Key values to create a Web Session on PingAccess.</span></span> <span data-ttu-id="a7c05-204">U kunt daarna Identiteitstoewijzing instellen en maken van een virtuele host, de site en de toepassing.</span><span class="sxs-lookup"><span data-stu-id="a7c05-204">After that, you can set up identity mapping and create a virtual host, site, and application.</span></span>

### <a name="test-your-app"></a><span data-ttu-id="a7c05-205">Uw app testen</span><span class="sxs-lookup"><span data-stu-id="a7c05-205">Test your app</span></span>

<span data-ttu-id="a7c05-206">Als u al deze stappen hebt voltooid, moet uw app actief en werkend.</span><span class="sxs-lookup"><span data-stu-id="a7c05-206">When you've completed all these steps, your app should be up and running.</span></span> <span data-ttu-id="a7c05-207">Als u wilt testen, open een browser en Ga naar de externe URL die u hebt gemaakt toen u de app in Azure hebt gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="a7c05-207">To test it, open a browser and navigate to the external URL that you created when you published the app in Azure.</span></span> <span data-ttu-id="a7c05-208">Aanmelden met de testaccount dat u hebt toegewezen aan de app.</span><span class="sxs-lookup"><span data-stu-id="a7c05-208">Sign in with the test account that you assigned to the app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7c05-209">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a7c05-209">Next steps</span></span>

- [<span data-ttu-id="a7c05-210">PingAccess configureren voor Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7c05-210">Configure PingAccess for Azure AD</span></span>](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html)
- [<span data-ttu-id="a7c05-211">Hoe biedt Azure AD-toepassingsproxy eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="a7c05-211">How does Azure AD Application Proxy provide single sign-on?</span></span>](application-proxy-sso-overview.md)
- [<span data-ttu-id="a7c05-212">Toepassingsproxy oplossen</span><span class="sxs-lookup"><span data-stu-id="a7c05-212">Troubleshoot Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)
