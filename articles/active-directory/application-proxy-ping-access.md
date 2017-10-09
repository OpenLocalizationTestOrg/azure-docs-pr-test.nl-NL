---
title: verificatie op basis van aaaHeader met PingAccess voor Azure AD-toepassingsproxy | Microsoft Docs
description: Toepassingen met PingAccess toepassingsproxy toosupport headers gebaseerde verificatie en publiceren.
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
ms.openlocfilehash: 38fe3e7a41a71f4ae6c75f014e44c722f773bd22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="header-based-authentication-for-single-sign-on-with-application-proxy-and-pingaccess"></a><span data-ttu-id="92a88-103">Verificatie op basis van een koptekst voor eenmalige aanmelding met toepassingsproxy en PingAccess</span><span class="sxs-lookup"><span data-stu-id="92a88-103">Header-based authentication for single sign-on with Application Proxy and PingAccess</span></span>

<span data-ttu-id="92a88-104">Azure Active Directory-toepassingsproxy en PingAccess hebben hun samen tooprovide Azure Active Directory-klanten met toegang tooeven meer toepassingen.</span><span class="sxs-lookup"><span data-stu-id="92a88-104">Azure Active Directory Application Proxy and PingAccess have partnered together tooprovide Azure Active Directory customers with access tooeven more applications.</span></span> <span data-ttu-id="92a88-105">PingAccess wordt uitgebreid Hallo [bestaande toepassingsproxy aanbiedingen](active-directory-application-proxy-get-started.md) tooinclude één aanmelding toegang tooapplications die headers voor verificatie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="92a88-105">PingAccess expands hello [existing Application Proxy offerings](active-directory-application-proxy-get-started.md) tooinclude single sign-on access tooapplications that use headers for authentication.</span></span>

## <a name="what-is-pingaccess-for-azure-ad"></a><span data-ttu-id="92a88-106">Wat is PingAccess voor Azure AD?</span><span class="sxs-lookup"><span data-stu-id="92a88-106">What is PingAccess for Azure AD?</span></span>

<span data-ttu-id="92a88-107">PingAccess voor Azure Active Directory is een aanbieding van PingAccess waarmee u toogive gebruikerstoegang en eenmalige aanmelding tooapplications die headers voor verificatie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="92a88-107">PingAccess for Azure Active Directory is an offering of PingAccess that enables you toogive users access and single sign-on tooapplications that use headers for authentication.</span></span> <span data-ttu-id="92a88-108">Toepassingsproxy behandelt deze apps zoals elke andere met behulp van Azure AD tooauthenticate toegang en vervolgens verkeer via Hallo-connectorservice wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="92a88-108">Application Proxy treats these apps like any other, using Azure AD tooauthenticate access and then passing traffic through hello connector service.</span></span> <span data-ttu-id="92a88-109">PingAccess bevindt zich voor het Hallo-apps en zet Hallo toegangstoken van Azure AD in een koptekst zodat Hallo toepassing hello verificatie in Hallo-indeling die kan gelezen ontvangt.</span><span class="sxs-lookup"><span data-stu-id="92a88-109">PingAccess sits in front of hello apps and translates hello access token from Azure AD into a header so that hello application receives hello authentication in hello format it can read.</span></span>

<span data-ttu-id="92a88-110">Uw gebruikers won't iets anders zien wanneer ze zich toouse uw zakelijke apps aanmelden.</span><span class="sxs-lookup"><span data-stu-id="92a88-110">Your users won’t notice anything different when they sign in toouse your corporate apps.</span></span> <span data-ttu-id="92a88-111">Ze kunnen nog steeds overal werken uit op elk apparaat.</span><span class="sxs-lookup"><span data-stu-id="92a88-111">They can still work from anywhere on any device.</span></span> 

<span data-ttu-id="92a88-112">Aangezien Hallo toepassingsproxy connectors extern verkeer tooall apps, ongeacht hun verificatietype directe, moeten ze tooload saldo blijven automatisch, maar ook.</span><span class="sxs-lookup"><span data-stu-id="92a88-112">Since hello Application Proxy connectors direct remote traffic tooall apps regardless of their authentication type, they’ll continue tooload balance automatically, as well.</span></span>

## <a name="how-do-i-get-access"></a><span data-ttu-id="92a88-113">Hoe krijg ik toegang?</span><span class="sxs-lookup"><span data-stu-id="92a88-113">How do I get access?</span></span>

<span data-ttu-id="92a88-114">Aangezien dit scenario wordt aangeboden via een samenwerking tussen Azure Active Directory en PingAccess, moet u licenties voor beide services.</span><span class="sxs-lookup"><span data-stu-id="92a88-114">Since this scenario is offered through a partnership between Azure Active Directory and PingAccess, you need licenses for both services.</span></span> <span data-ttu-id="92a88-115">Azure Active Directory Premium-abonnementen bevatten echter een PingAccess standaardlicentie die betrekking heeft op up too20 toepassingen.</span><span class="sxs-lookup"><span data-stu-id="92a88-115">However, Azure Active Directory Premium subscriptions include a basic PingAccess license that covers up too20 applications.</span></span> <span data-ttu-id="92a88-116">Als u toopublish meer dan 20 header-toepassingen moet, kunt u een extra licentie aanschaffen bij PingAccess.</span><span class="sxs-lookup"><span data-stu-id="92a88-116">If you need toopublish more than 20 header-based applications, you can purchase an additional license from PingAccess.</span></span> 

<span data-ttu-id="92a88-117">Zie [Azure Active Directory-edities](active-directory-editions.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="92a88-117">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

## <a name="publish-your-application-in-azure"></a><span data-ttu-id="92a88-118">Uw toepassing publiceren in Azure</span><span class="sxs-lookup"><span data-stu-id="92a88-118">Publish your application in Azure</span></span>

<span data-ttu-id="92a88-119">In dit artikel is bedoeld voor personen die een app met dit scenario voor Hallo eerst wilt publiceren.</span><span class="sxs-lookup"><span data-stu-id="92a88-119">This article is intended for people who are publishing an app with this scenario for hello first time.</span></span> <span data-ttu-id="92a88-120">Er wordt uitgelegd hoe tooget met de toepassings- en PingAccess, Daarnaast toohello publishing stappen gestart.</span><span class="sxs-lookup"><span data-stu-id="92a88-120">It walks through how tooget started with both Application and PingAccess, in addition toohello publishing steps.</span></span> <span data-ttu-id="92a88-121">Als u beide services al hebt geconfigureerd, maar u wilt dat een refresher op Hallo stappen publiceren, kunt u overslaan Hallo-connector installeren en te verplaatsen op[toevoegen van uw app tooAzure AD met toepassingsproxy](#add-your-app-to-Azure-AD-with-Application-Proxy).</span><span class="sxs-lookup"><span data-stu-id="92a88-121">If you’ve already configured both services but want a refresher on hello publishing steps, you can skip hello connector installation and move on too[Add your app tooAzure AD with Application Proxy](#add-your-app-to-Azure-AD-with-Application-Proxy).</span></span>

>[!NOTE]
><span data-ttu-id="92a88-122">Omdat dit scenario een verbinding tussen Azure AD is en PingAccess, aantal Hallo instructies aanwezig zijn op Hallo identiteit van de Ping-site.</span><span class="sxs-lookup"><span data-stu-id="92a88-122">Since this scenario is a partnership between Azure AD and PingAccess, some of hello instructions exist on hello Ping Identity site.</span></span>

### <a name="install-an-application-proxy-connector"></a><span data-ttu-id="92a88-123">Een Application Proxy connector installeren</span><span class="sxs-lookup"><span data-stu-id="92a88-123">Install an Application Proxy connector</span></span>

<span data-ttu-id="92a88-124">Als u al Application Proxy ingeschakeld hebt en hebt een connector is geïnstalleerd, kunt u deze sectie overslaan en te verplaatsen op[toevoegen van uw app tooAzure AD met toepassingsproxy](#add-your-app-to-azure-ad-with-application-proxy).</span><span class="sxs-lookup"><span data-stu-id="92a88-124">If you already have Application Proxy enabled, and have a connector installed, you can skip this section and move on too[Add your app tooAzure AD with Application Proxy](#add-your-app-to-azure-ad-with-application-proxy).</span></span>

<span data-ttu-id="92a88-125">Hallo Application Proxy connector is een Windows Server-service die Hallo verkeer van uw werknemers extern tooyour stuurt gepubliceerde apps.</span><span class="sxs-lookup"><span data-stu-id="92a88-125">hello Application Proxy connector is a Windows Server service that directs hello traffic from your remote employees tooyour published apps.</span></span> <span data-ttu-id="92a88-126">Zie voor meer installatie-instructies, [toepassingsproxy inschakelen in Azure-portal Hallo](active-directory-application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="92a88-126">For more detailed installation instructions, see [Enable Application Proxy in hello Azure portal](active-directory-application-proxy-enable.md).</span></span>

1. <span data-ttu-id="92a88-127">Meld u aan toohello [Azure-portal](https://portal.azure.com) als globale beheerder.</span><span class="sxs-lookup"><span data-stu-id="92a88-127">Sign in toohello [Azure portal](https://portal.azure.com) as a global administrator.</span></span>
2. <span data-ttu-id="92a88-128">Selecteer **Azure Active Directory** > **toepassingsproxy**.</span><span class="sxs-lookup"><span data-stu-id="92a88-128">Select **Azure Active Directory** > **Application proxy**.</span></span>
3. <span data-ttu-id="92a88-129">Selecteer **Connector downloaden** toostart Hallo Application Proxy connector downloaden.</span><span class="sxs-lookup"><span data-stu-id="92a88-129">Select **Download Connector** toostart hello Application Proxy connector download.</span></span> <span data-ttu-id="92a88-130">Hallo-installatie-instructies.</span><span class="sxs-lookup"><span data-stu-id="92a88-130">Follow hello installation instructions.</span></span>

   ![Toepassingsproxy inschakelen en Hallo connector downloaden](./media/application-proxy-ping-access/install-connector.png)

4. <span data-ttu-id="92a88-132">Hallo connector downloaden moet automatisch toepassingsproxy inschakelen voor uw directory, maar als u dit niet kunt selecteren **Enable Application Proxy**.</span><span class="sxs-lookup"><span data-stu-id="92a88-132">Downloading hello connector should automatically enable Application Proxy for your directory, but if not you can select **Enable Application Proxy**.</span></span>


### <a name="add-your-app-tooazure-ad-with-application-proxy"></a><span data-ttu-id="92a88-133">Uw app tooAzure AD met toepassingsproxy toevoegen</span><span class="sxs-lookup"><span data-stu-id="92a88-133">Add your app tooAzure AD with Application Proxy</span></span>

<span data-ttu-id="92a88-134">Er zijn twee acties, moet u tootake in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="92a88-134">There are two actions you need tootake in hello Azure portal.</span></span> <span data-ttu-id="92a88-135">U moet eerst uw toepassing met toepassingsproxy toopublish.</span><span class="sxs-lookup"><span data-stu-id="92a88-135">First, you need toopublish your application with Application Proxy.</span></span> <span data-ttu-id="92a88-136">Vervolgens moet u toocollect enige informatie over het Hallo-app die u kunt tijdens Hallo PingAccess stappen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="92a88-136">Then, you need toocollect some information about hello app that you can use during hello PingAccess steps.</span></span>

<span data-ttu-id="92a88-137">Volg deze stappen toopublish uw app.</span><span class="sxs-lookup"><span data-stu-id="92a88-137">Follow these steps toopublish your app.</span></span> <span data-ttu-id="92a88-138">Voor een meer overzicht van de stappen 1-8, Zie gedetailleerde [toepassingen publiceren met Azure AD-toepassingsproxy](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="92a88-138">For a more detailed walkthrough of steps 1-8, see [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

1. <span data-ttu-id="92a88-139">Als dat niet in de laatste sectie Hallo aanmelden toohello [Azure-portal](https://portal.azure.com) als globale beheerder.</span><span class="sxs-lookup"><span data-stu-id="92a88-139">If you didn't in hello last section, sign in toohello [Azure portal](https://portal.azure.com) as a global administrator.</span></span>
2. <span data-ttu-id="92a88-140">Selecteer **Azure Active Directory** > **bedrijfstoepassingen**.</span><span class="sxs-lookup"><span data-stu-id="92a88-140">Select **Azure Active Directory** > **Enterprise applications**.</span></span>
3. <span data-ttu-id="92a88-141">Selecteer **toevoegen** Hallo boven aan het Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="92a88-141">Select **Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="92a88-142">Selecteer **On-premises toepassing**.</span><span class="sxs-lookup"><span data-stu-id="92a88-142">Select **On-premises application**.</span></span>
5. <span data-ttu-id="92a88-143">Vul de velden Hallo vereist met informatie over uw nieuwe app.</span><span class="sxs-lookup"><span data-stu-id="92a88-143">Fill out hello required fields with information about your new app.</span></span> <span data-ttu-id="92a88-144">Hallo volgen richtlijnen voor het Hallo-instellingen gebruiken:</span><span class="sxs-lookup"><span data-stu-id="92a88-144">Use hello following guidance for hello settings:</span></span>
   - <span data-ttu-id="92a88-145">**Interne URL**: normaal u Hallo-URL die u toohello-app-aanmelding op de pagina als u in het bedrijfsnetwerk Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="92a88-145">**Internal URL**: Normally you provide hello URL that takes you toohello app’s sign in page when you’re on hello corporate network.</span></span> <span data-ttu-id="92a88-146">Voor dit scenario moet Hallo connector tootreat hello PingAccess proxy als Hallo voorpagina van Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="92a88-146">For this scenario hello connector needs tootreat hello PingAccess proxy as hello front page of hello app.</span></span> <span data-ttu-id="92a88-147">Gebruik de volgende notatie: `https://<host name of your PA server>:<port>`.</span><span class="sxs-lookup"><span data-stu-id="92a88-147">Use this format: `https://<host name of your PA server>:<port>`.</span></span> <span data-ttu-id="92a88-148">Hallo-poort is 3000 standaard, maar u kunt deze configureren in PingAccess.</span><span class="sxs-lookup"><span data-stu-id="92a88-148">hello port is 3000 by default, but you can configure it in PingAccess.</span></span>
   - <span data-ttu-id="92a88-149">**Methode voor verificatie vooraf**: Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="92a88-149">**Pre-authentication method**: Azure Active Directory</span></span>
   - <span data-ttu-id="92a88-150">**URL in de Headers vertalen**: Nee</span><span class="sxs-lookup"><span data-stu-id="92a88-150">**Translate URL in Headers**: No</span></span>

   >[!NOTE]
   ><span data-ttu-id="92a88-151">Als dit uw eerste toepassing, gebruik van poort 3000 toostart en keert u terug tooupdate deze instelling als u de configuratie van uw PingAccess wijzigt.</span><span class="sxs-lookup"><span data-stu-id="92a88-151">If this is your first application, use port 3000 toostart and come back tooupdate this setting if you change your PingAccess configuration.</span></span> <span data-ttu-id="92a88-152">Als dit uw app tweede of hoger, moet dit toomatch Hallo Listener die u hebt geconfigureerd in PingAccess.</span><span class="sxs-lookup"><span data-stu-id="92a88-152">If this is your second or later app, this will need toomatch hello Listener you’ve configured in PingAccess.</span></span> <span data-ttu-id="92a88-153">Meer informatie over [luisteraars in PingAccess](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html).</span><span class="sxs-lookup"><span data-stu-id="92a88-153">Learn more about [listeners in PingAccess](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html).</span></span>

6. <span data-ttu-id="92a88-154">Selecteer **toevoegen** Hallo Hallo blade onderaan in.</span><span class="sxs-lookup"><span data-stu-id="92a88-154">Select **Add** at hello bottom of hello blade.</span></span> <span data-ttu-id="92a88-155">Uw toepassing wordt toegevoegd en Hallo snel startmenu wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="92a88-155">Your application is added, and hello quick start menu opens.</span></span>
7. <span data-ttu-id="92a88-156">Selecteer in het menu snelle start Hallo **een gebruiker toewijzen voor het testen van**, en ten minste één gebruiker toohello toepassing toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="92a88-156">In hello quick start menu, select **Assign a user for testing**, and add at least one user toohello application.</span></span> <span data-ttu-id="92a88-157">Zorg ervoor dat dit testaccount toegang toohello on-premises toepassing.</span><span class="sxs-lookup"><span data-stu-id="92a88-157">Make sure this test account has access toohello on-premises application.</span></span>
8. <span data-ttu-id="92a88-158">Selecteer **toewijzen** toosave Hallo test de gebruiker is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="92a88-158">Select **Assign** toosave hello test user assignment.</span></span>
9. <span data-ttu-id="92a88-159">Selecteer op de blade Hallo app management, **eenmalige aanmelding**.</span><span class="sxs-lookup"><span data-stu-id="92a88-159">On hello app management blade, select **Single sign-on**.</span></span>
10. <span data-ttu-id="92a88-160">Kies **headers gebaseerde aanmelding** uit de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="92a88-160">Choose **Header-based sign-on** from hello drop-down menu.</span></span> <span data-ttu-id="92a88-161">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="92a88-161">Select **Save**.</span></span>

   >[!TIP]
   ><span data-ttu-id="92a88-162">Als dit de eerste keer is op basis van een koptekst eenmalige aanmelding, moet u tooinstall PingAccess.</span><span class="sxs-lookup"><span data-stu-id="92a88-162">If this is your first time using header-based single sign-on, you need tooinstall PingAccess.</span></span> <span data-ttu-id="92a88-163">toomake ervoor dat uw Azure-abonnement is automatisch gekoppeld aan uw PingAccess-installatie Hallo-verbinding op deze pagina voor eenmalige aanmelding toodownload PingAccess gebruiken.</span><span class="sxs-lookup"><span data-stu-id="92a88-163">toomake sure your Azure subscription is automatically associated with your PingAccess installation, use hello link on this single sign-on page toodownload PingAccess.</span></span> <span data-ttu-id="92a88-164">U kunt nu Hallo downloadsite openen of toothis pagina later terugkomen.</span><span class="sxs-lookup"><span data-stu-id="92a88-164">You can open hello download site now, or come back toothis page later.</span></span> 

   ![Selecteer op basis van een koptekst eenmalige aanmelding](./media/application-proxy-ping-access/sso-header.PNG)

11. <span data-ttu-id="92a88-166">Hallo Enterprise toepassingen blade sluiten of alle Hallo manier toohello links tooreturn toohello Azure Active Directory menu bladeren.</span><span class="sxs-lookup"><span data-stu-id="92a88-166">Close hello Enterprise applications blade or scroll all hello way toohello left tooreturn toohello Azure Active Directory menu.</span></span>
12. <span data-ttu-id="92a88-167">Selecteer **App registraties**.</span><span class="sxs-lookup"><span data-stu-id="92a88-167">Select **App registrations**.</span></span>

   ![Selecteer de App-registraties](./media/application-proxy-ping-access/app-registrations.png)

13. <span data-ttu-id="92a88-169">Selecteer Hallo-app die u zojuist hebt toegevoegd, klikt u vervolgens **antwoord-URL's**.</span><span class="sxs-lookup"><span data-stu-id="92a88-169">Select hello app you just added, then **Reply URLs**.</span></span>

   ![Selecteer de antwoord-URL 's](./media/application-proxy-ping-access/reply-urls.png)

14. <span data-ttu-id="92a88-171">Controleer de toosee als externe URL Hallo die u toegewezen tooyour app in stap 5 in de lijst met Hallo antwoord-URL's.</span><span class="sxs-lookup"><span data-stu-id="92a88-171">Check toosee if hello external URL that you assigned tooyour app in step 5 is in hello Reply URLs list.</span></span> <span data-ttu-id="92a88-172">Als dit niet het geval is, moet u deze nu toevoegen.</span><span class="sxs-lookup"><span data-stu-id="92a88-172">If it’s not, add it now.</span></span>
15. <span data-ttu-id="92a88-173">Selecteer op de blade Hallo app-instellingen, **vereist machtigingen**.</span><span class="sxs-lookup"><span data-stu-id="92a88-173">On hello app settings blade, select **Required permissions**.</span></span>

  ![Selecteer de vereiste machtigingen](./media/application-proxy-ping-access/required-permissions.png)

16. <span data-ttu-id="92a88-175">Selecteer **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="92a88-175">Select **Add**.</span></span> <span data-ttu-id="92a88-176">Kies voor Hallo API, **Windows Azure Active Directory**, klikt u vervolgens **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="92a88-176">For hello API, choose **Windows Azure Active Directory**, then **Select**.</span></span> <span data-ttu-id="92a88-177">Hallo-machtigingen, kiest u **lezen en schrijven van alle toepassingen** en **aanmelden en gebruikersprofiel lezen**, vervolgens **Selecteer** en **gedaan**.</span><span class="sxs-lookup"><span data-stu-id="92a88-177">For hello permissions, choose **Read and write all applications** and **Sign in and read user profile**, then **Select** and **Done**.</span></span>  

  ![Selecteer machtigingen](./media/application-proxy-ping-access/select-permissions.png)

### <a name="collect-information-for-hello-pingaccess-steps"></a><span data-ttu-id="92a88-179">Verzamelen van informatie voor Hallo PingAccess stappen</span><span class="sxs-lookup"><span data-stu-id="92a88-179">Collect information for hello PingAccess steps</span></span>

1. <span data-ttu-id="92a88-180">Selecteer op de blade van uw app-instellingen **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="92a88-180">On your app settings blade, select **Properties**.</span></span> 

  ![Eigenschappen selecteren](./media/application-proxy-ping-access/properties.png)

2. <span data-ttu-id="92a88-182">Hallo opslaan **toepassings-Id** waarde.</span><span class="sxs-lookup"><span data-stu-id="92a88-182">Save hello **Application Id** value.</span></span> <span data-ttu-id="92a88-183">Dit wordt gebruikt voor Hallo client-ID wanneer u PingAccess configureert.</span><span class="sxs-lookup"><span data-stu-id="92a88-183">This is used for hello client ID when you configure PingAccess.</span></span>
3. <span data-ttu-id="92a88-184">Selecteer op de blade Hallo app-instellingen, **sleutels**.</span><span class="sxs-lookup"><span data-stu-id="92a88-184">On hello app settings blade, select **Keys**.</span></span>

  ![Selecteer sleutels](./media/application-proxy-ping-access/Keys.png)

4. <span data-ttu-id="92a88-186">Een sleutel door te voeren van een sleutel beschrijving en een vervaldatum kiezen uit de vervolgkeuzelijst Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="92a88-186">Create a key by entering a key description and choosing an expiration date from hello drop-down menu.</span></span>
5. <span data-ttu-id="92a88-187">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="92a88-187">Select **Save**.</span></span> <span data-ttu-id="92a88-188">Een GUID wordt weergegeven in Hallo **waarde** veld.</span><span class="sxs-lookup"><span data-stu-id="92a88-188">A GUID appears in hello **Value** field.</span></span>

  <span data-ttu-id="92a88-189">Sla deze waarde, als u niet kunt toosee het opnieuw nadat u dit venster nu sluiten.</span><span class="sxs-lookup"><span data-stu-id="92a88-189">Save this value now, as you won’t be able toosee it again after you close this window.</span></span>

  ![Maak een nieuwe sleutel](./media/application-proxy-ping-access/create-keys.png)

6. <span data-ttu-id="92a88-191">Hallo App registraties blade sluiten of alle Hallo manier toohello links tooreturn toohello Azure Active Directory menu bladeren.</span><span class="sxs-lookup"><span data-stu-id="92a88-191">Close hello App registrations blade or scroll all hello way toohello left tooreturn toohello Azure Active Directory menu.</span></span>
7. <span data-ttu-id="92a88-192">Selecteer **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="92a88-192">Select **Properties**.</span></span>
8. <span data-ttu-id="92a88-193">Hallo opslaan **map-ID** GUID.</span><span class="sxs-lookup"><span data-stu-id="92a88-193">Save hello **Directory ID** GUID.</span></span>

### <a name="optional---update-graphapi-toosend-custom-fields"></a><span data-ttu-id="92a88-194">Optioneel - Update GraphAPI toosend aangepaste velden</span><span class="sxs-lookup"><span data-stu-id="92a88-194">Optional - Update GraphAPI toosend custom fields</span></span>

<span data-ttu-id="92a88-195">Zie voor een lijst van beveiligingstokens die door Azure AD voor verificatie verzonden, [Azure AD-tokenverwijzing](./develop/active-directory-token-and-claims.md).</span><span class="sxs-lookup"><span data-stu-id="92a88-195">For a list of security tokens that Azure AD sends for authentication, see [Azure AD token reference](./develop/active-directory-token-and-claims.md).</span></span> <span data-ttu-id="92a88-196">Als u een aangepaste claim die door andere tokens verzonden moet, gebruikt u GraphAPI tooset Hallo app veld *acceptMappedClaims* te**True**.</span><span class="sxs-lookup"><span data-stu-id="92a88-196">If you need a custom claim that sends other tokens, use GraphAPI tooset hello app field *acceptMappedClaims* too**True**.</span></span> <span data-ttu-id="92a88-197">U kunt deze configuratie Azure AD Graph Explorer of MS Graph toomake.</span><span class="sxs-lookup"><span data-stu-id="92a88-197">You can use either Azure AD Graph Explorer or MS Graph toomake this configuration.</span></span> 

<span data-ttu-id="92a88-198">In dit voorbeeld wordt een grafiek Explorer:</span><span class="sxs-lookup"><span data-stu-id="92a88-198">This example uses Graph Explorer:</span></span>

```
PATCH https://graph.windows.net/myorganization/applications/<object_id_GUID_of_your_application> 

{
  "acceptMappedClaims":true
}
```

## <a name="download-pingaccess-and-configure-your-app"></a><span data-ttu-id="92a88-199">PingAccess downloaden en configureren van uw app</span><span class="sxs-lookup"><span data-stu-id="92a88-199">Download PingAccess and configure your app</span></span>

<span data-ttu-id="92a88-200">Nu dat u alle hello Azure Active Directory setup stappen hebt voltooid, kunt u op tooconfiguring PingAccess.</span><span class="sxs-lookup"><span data-stu-id="92a88-200">Now that you've completed all hello Azure Active Directory setup steps, you can move on tooconfiguring PingAccess.</span></span> 

<span data-ttu-id="92a88-201">Hallo gedetailleerde stappen voor het Hallo PingAccess deel uitmaken van dit scenario blijven Hallo identiteit van de Ping-documentatie, [PingAccess configureren voor Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html).</span><span class="sxs-lookup"><span data-stu-id="92a88-201">hello detailed steps for hello PingAccess part of this scenario continue in hello Ping Identity documentation, [Configure PingAccess for Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html).</span></span>

<span data-ttu-id="92a88-202">Deze stappen doorlopen Hallo-proces voor het ophalen van een account PingAccess als u er nog geen hebt, Hallo PingAccess Server installeren en een Azure AD OIDC providerverbinding maken met Hallo map-ID die u hebt gekopieerd uit hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="92a88-202">Those steps walk you through hello process of getting a PingAccess account if you don't already have one, installing hello PingAccess Server, and creating an Azure AD OIDC Provider connection with hello Directory ID that you copied from hello Azure portal.</span></span> <span data-ttu-id="92a88-203">Vervolgens gebruikt u Hallo toepassings-ID en sleutel waarden toocreate een websessie op PingAccess.</span><span class="sxs-lookup"><span data-stu-id="92a88-203">Then, you use hello Application ID and Key values toocreate a Web Session on PingAccess.</span></span> <span data-ttu-id="92a88-204">U kunt daarna Identiteitstoewijzing instellen en maken van een virtuele host, de site en de toepassing.</span><span class="sxs-lookup"><span data-stu-id="92a88-204">After that, you can set up identity mapping and create a virtual host, site, and application.</span></span>

### <a name="test-your-app"></a><span data-ttu-id="92a88-205">Uw app testen</span><span class="sxs-lookup"><span data-stu-id="92a88-205">Test your app</span></span>

<span data-ttu-id="92a88-206">Als u al deze stappen hebt voltooid, moet uw app actief en werkend.</span><span class="sxs-lookup"><span data-stu-id="92a88-206">When you've completed all these steps, your app should be up and running.</span></span> <span data-ttu-id="92a88-207">tootest, open een browser en ga toohello externe URL die u hebt gemaakt toen u Hallo-app in Azure hebt gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="92a88-207">tootest it, open a browser and navigate toohello external URL that you created when you published hello app in Azure.</span></span> <span data-ttu-id="92a88-208">Meld u aan met Hallo testaccount die toegewezen toohello u app.</span><span class="sxs-lookup"><span data-stu-id="92a88-208">Sign in with hello test account that you assigned toohello app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="92a88-209">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="92a88-209">Next steps</span></span>

- [<span data-ttu-id="92a88-210">PingAccess configureren voor Azure AD</span><span class="sxs-lookup"><span data-stu-id="92a88-210">Configure PingAccess for Azure AD</span></span>](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html)
- [<span data-ttu-id="92a88-211">Hoe biedt Azure AD-toepassingsproxy eenmalige aanmelding</span><span class="sxs-lookup"><span data-stu-id="92a88-211">How does Azure AD Application Proxy provide single sign-on?</span></span>](application-proxy-sso-overview.md)
- [<span data-ttu-id="92a88-212">Toepassingsproxy oplossen</span><span class="sxs-lookup"><span data-stu-id="92a88-212">Troubleshoot Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)
