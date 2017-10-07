---
title: aaaMFA software development kit voor aangepaste apps | Microsoft Docs
description: Dit artikel laat zien hoe Hallo verificatie van Azure MFA-SDK tooenable in twee stappen voor uw aangepaste apps toodownload en het gebruik.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 1c152f67-be02-42a5-a0c7-246fb6b34377
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: 10e02e844bf3928575bfca79dbc34717a31a08b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="building-multi-factor-authentication-into-custom-apps-sdk"></a><span data-ttu-id="ee19e-103">Gebouw multi-factor Authentication in aangepaste Apps (SDK)</span><span class="sxs-lookup"><span data-stu-id="ee19e-103">Building Multi-Factor Authentication into Custom Apps (SDK)</span></span>

<span data-ttu-id="ee19e-104">Hello Azure multi-factor Authentication Software Development Kit (SDK) kunt die u de verificatie in twee stappen rechtstreeks in bouwen Hallo aanmelden of transactie verwerkt van toepassingen in uw Azure AD-tenant.</span><span class="sxs-lookup"><span data-stu-id="ee19e-104">hello Azure Multi-Factor Authentication Software Development Kit (SDK) lets you build two-step verification directly into hello sign-in or transaction processes of applications in your Azure AD tenant.</span></span>

<span data-ttu-id="ee19e-105">Hallo multi-factor Authentication SDK is beschikbaar voor C#, Visual Basic (.NET), Java, Perl, PHP en Ruby.</span><span class="sxs-lookup"><span data-stu-id="ee19e-105">hello Multi-Factor Authentication SDK is available for C#, Visual Basic (.NET), Java, Perl, PHP, and Ruby.</span></span> <span data-ttu-id="ee19e-106">Hallo SDK biedt een thin wrapper rond verificatie in twee stappen.</span><span class="sxs-lookup"><span data-stu-id="ee19e-106">hello SDK provides a thin wrapper around two-step verification.</span></span> <span data-ttu-id="ee19e-107">Het bevat alles wat dat u moet toowrite uw code, inclusief opmerkingen broncodebestanden, bijvoorbeeld bestanden en een gedetailleerde Leesmij-bestand.</span><span class="sxs-lookup"><span data-stu-id="ee19e-107">It includes everything you need toowrite your code, including commented source code files, example files, and a detailed ReadMe file.</span></span> <span data-ttu-id="ee19e-108">Elke SDK bevat ook een certificaat en de persoonlijke sleutel voor het versleutelen van transacties die unieke tooyour multi-factor Authentication-Provider zijn.</span><span class="sxs-lookup"><span data-stu-id="ee19e-108">Each SDK also includes a certificate and private key for encrypting transactions that are unique tooyour Multi-Factor Authentication Provider.</span></span> <span data-ttu-id="ee19e-109">Als u een provider hebt, kunt u Hallo SDK in zoveel talen en indelingen downloaden als u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="ee19e-109">As long as you have a provider, you can download hello SDK in as many languages and formats as you need.</span></span>

<span data-ttu-id="ee19e-110">Hallo-structuur van Hallo API's in Hallo multi-factor Authentication SDK is eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="ee19e-110">hello structure of hello APIs in hello Multi-Factor Authentication SDK is simple.</span></span> <span data-ttu-id="ee19e-111">Controleer één functie tooan API met Hallo meerledige optie parameters (zoals de verificatie-modus) en gegevens van de gebruiker (zoals Hallo telefoon nummer toocall of Hallo PINCODE nummer toovalidate) aanroepen.</span><span class="sxs-lookup"><span data-stu-id="ee19e-111">Make a single function call tooan API with hello multi-factor option parameters (like verification mode) and user data (like hello telephone number toocall or hello PIN number toovalidate).</span></span> <span data-ttu-id="ee19e-112">Hallo API's vertalen Hallo functieaanroep in web services aanvragen toohello cloud-gebaseerde Azure multi-factor Authentication Service.</span><span class="sxs-lookup"><span data-stu-id="ee19e-112">hello APIs translate hello function call into web services requests toohello cloud-based Azure Multi-Factor Authentication Service.</span></span> <span data-ttu-id="ee19e-113">Alle aanroepen moeten een verwijzing toohello persoonlijk certificaat dat is opgenomen in elke SDK bevatten.</span><span class="sxs-lookup"><span data-stu-id="ee19e-113">All calls must include a reference toohello private certificate that is included in every SDK.</span></span>

<span data-ttu-id="ee19e-114">Omdat Hallo API's toegang toousers geregistreerd in Azure Active Directory niet hebt, moet u gebruikersgegevens in een bestand of de database opgeven.</span><span class="sxs-lookup"><span data-stu-id="ee19e-114">Because hello APIs do not have access toousers registered in Azure Active Directory, you must provide user information in a file or database.</span></span> <span data-ttu-id="ee19e-115">Ook Hallo API's bieden geen informatie over de beheerfuncties van inschrijving of gebruiker, dus moet u toobuild deze processen in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="ee19e-115">Also, hello APIs do not provide enrollment or user management features, so you need toobuild these processes into your application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee19e-116">toodownload Hallo SDK, moet u een Azure multi-factor Authentication-Provider toocreate zelfs als u Azure MFA, AAD Premium of EMS-licenties hebt.</span><span class="sxs-lookup"><span data-stu-id="ee19e-116">toodownload hello SDK, you need toocreate an Azure Multi-Factor Auth Provider even if you have Azure MFA, AAD Premium, or EMS licenses.</span></span> <span data-ttu-id="ee19e-117">Als u een Azure multi-factor Authentication-Provider voor dit doel maken en hebt al licenties, zorg ervoor dat toocreate Hallo Provider Hello **Per ingeschakelde gebruiker** model.</span><span class="sxs-lookup"><span data-stu-id="ee19e-117">If you create an Azure Multi-Factor Auth Provider for this purpose and already have licenses, make sure toocreate hello Provider with hello **Per Enabled User** model.</span></span> <span data-ttu-id="ee19e-118">Koppel vervolgens Hallo Provider toohello map waarin hello Azure MFA, Azure AD Premium of EMS-licenties.</span><span class="sxs-lookup"><span data-stu-id="ee19e-118">Then, link hello Provider toohello directory that contains hello Azure MFA, Azure AD Premium, or EMS licenses.</span></span> <span data-ttu-id="ee19e-119">Deze configuratie zorgt ervoor dat u wordt alleen gefactureerd als u meer unieke gebruikers met behulp van Hallo SDK dan het aantal licenties dat u bezit Hallo hebt.</span><span class="sxs-lookup"><span data-stu-id="ee19e-119">This configuration ensures that you are only billed if you have more unique users using hello SDK than hello number of licenses you own.</span></span>


## <a name="download-hello-sdk"></a><span data-ttu-id="ee19e-120">Hallo SDK downloaden</span><span class="sxs-lookup"><span data-stu-id="ee19e-120">Download hello SDK</span></span>
<span data-ttu-id="ee19e-121">Hello Azure multi-factor Authentication SDK downloaden vereist een [Azure multi-factor Authentication-Provider](multi-factor-authentication-get-started-auth-provider.md).</span><span class="sxs-lookup"><span data-stu-id="ee19e-121">Downloading hello Azure Multi-Factor SDK requires an [Azure Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md).</span></span>  <span data-ttu-id="ee19e-122">Hiervoor moet een volledige Azure-abonnement, zelfs als het eigendom van Azure MFA, Azure AD Premium of Enterprise Mobility Suite licenties zijn.</span><span class="sxs-lookup"><span data-stu-id="ee19e-122">This requires a full Azure subscription, even if Azure MFA, Azure AD Premium, or Enterprise Mobility Suite licenses are owned.</span></span>  <span data-ttu-id="ee19e-123">toodownload hello SDK, navigeer toohello multi-factor-beheerportal.</span><span class="sxs-lookup"><span data-stu-id="ee19e-123">toodownload hello SDK, navigate toohello Multi-Factor Management Portal.</span></span> <span data-ttu-id="ee19e-124">U kunt Hallo portal door het beheer van Hallo multi-factor Auth Provider rechtstreeks of door te klikken op Hallo bereiken **"Ga toohello portal"** koppeling op de pagina instellingen Hallo MFA-service.</span><span class="sxs-lookup"><span data-stu-id="ee19e-124">You can reach hello portal either by managing hello Multi-Factor Auth Provider directly, or by clicking hello **"Go toohello portal"** link on hello MFA service settings page.</span></span>

### <a name="download-from-hello-azure-classic-portal"></a><span data-ttu-id="ee19e-125">Downloaden van Hallo klassieke Azure-portal</span><span class="sxs-lookup"><span data-stu-id="ee19e-125">Download from hello Azure classic portal</span></span>
1. <span data-ttu-id="ee19e-126">Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com) als beheerder.</span><span class="sxs-lookup"><span data-stu-id="ee19e-126">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) as an Administrator.</span></span>
2. <span data-ttu-id="ee19e-127">Selecteer aan de linkerkant Hallo **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ee19e-127">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="ee19e-128">Op de pagina van het Hallo Active Directory, op de bovenste Selecteer Hallo **multi-factor Auth-Providers**</span><span class="sxs-lookup"><span data-stu-id="ee19e-128">On hello Active Directory page, at hello top select **Multi-Factor Auth Providers**</span></span>
4. <span data-ttu-id="ee19e-129">Selecteer onderaan Hallo **beheren**.</span><span class="sxs-lookup"><span data-stu-id="ee19e-129">At hello bottom select **Manage**.</span></span> <span data-ttu-id="ee19e-130">Er wordt een nieuwe pagina geopend.</span><span class="sxs-lookup"><span data-stu-id="ee19e-130">A new page opens.</span></span>
5. <span data-ttu-id="ee19e-131">Klik op Hallo links onderin Hallo **SDK**.</span><span class="sxs-lookup"><span data-stu-id="ee19e-131">On hello left, at hello bottom, click **SDK**.</span></span>
   <span data-ttu-id="ee19e-132"><center>![Downloaden](./media/multi-factor-authentication-sdk/download.png)</center></span><span class="sxs-lookup"><span data-stu-id="ee19e-132"><center>![Download](./media/multi-factor-authentication-sdk/download.png)</center></span></span>
6. <span data-ttu-id="ee19e-133">Selecteer Hallo gewenste taal en klikt u op één Hallo gekoppeld downloadkoppelingen.</span><span class="sxs-lookup"><span data-stu-id="ee19e-133">Select hello language you want and click one hello associated download links.</span></span>
7. <span data-ttu-id="ee19e-134">Sla Hallo downloaden.</span><span class="sxs-lookup"><span data-stu-id="ee19e-134">Save hello download.</span></span>

### <a name="download-from-hello-service-settings"></a><span data-ttu-id="ee19e-135">Downloaden van Hallo service-instellingen</span><span class="sxs-lookup"><span data-stu-id="ee19e-135">Download from hello service settings</span></span>
1. <span data-ttu-id="ee19e-136">Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com) als beheerder.</span><span class="sxs-lookup"><span data-stu-id="ee19e-136">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) as an Administrator.</span></span>
2. <span data-ttu-id="ee19e-137">Selecteer aan de linkerkant Hallo **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ee19e-137">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="ee19e-138">Dubbelklik op uw exemplaar van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ee19e-138">Double-click your instance of Azure AD.</span></span>
4. <span data-ttu-id="ee19e-139">Op Hallo bovenaan op **configureren**</span><span class="sxs-lookup"><span data-stu-id="ee19e-139">At hello top click **Configure**</span></span>
5. <span data-ttu-id="ee19e-140">Selecteer onder multi-factor authentication **service-instellingen beheren**
   ![downloaden](./media/multi-factor-authentication-sdk/download2.png)</span><span class="sxs-lookup"><span data-stu-id="ee19e-140">Under multi-factor authentication, select **Manage service settings**
![Download](./media/multi-factor-authentication-sdk/download2.png)</span></span>
6. <span data-ttu-id="ee19e-141">Klik op Hallo services instellingenpagina onderaan Hallo welkomstscherm op **Ga toohello portal**.</span><span class="sxs-lookup"><span data-stu-id="ee19e-141">On hello services settings page, at hello bottom of hello screen click **Go toohello portal**.</span></span> <span data-ttu-id="ee19e-142">Er wordt een nieuwe pagina geopend.</span><span class="sxs-lookup"><span data-stu-id="ee19e-142">A new page opens.</span></span>
   <span data-ttu-id="ee19e-143">![Downloaden](./media/multi-factor-authentication-sdk/download3a.png)</span><span class="sxs-lookup"><span data-stu-id="ee19e-143">![Download](./media/multi-factor-authentication-sdk/download3a.png)</span></span>
7. <span data-ttu-id="ee19e-144">Klik op Hallo links onderin Hallo **SDK**.</span><span class="sxs-lookup"><span data-stu-id="ee19e-144">On hello left, at hello bottom, click **SDK**.</span></span>
8. <span data-ttu-id="ee19e-145">Selecteer Hallo gewenste taal en klikt u op één Hallo gekoppeld downloadkoppelingen.</span><span class="sxs-lookup"><span data-stu-id="ee19e-145">Select hello language you want and click one hello associated download links.</span></span>
9. <span data-ttu-id="ee19e-146">Sla Hallo downloaden.</span><span class="sxs-lookup"><span data-stu-id="ee19e-146">Save hello download.</span></span>

## <a name="whats-in-hello-sdk"></a><span data-ttu-id="ee19e-147">Wat is er in Hallo SDK</span><span class="sxs-lookup"><span data-stu-id="ee19e-147">What's in hello SDK</span></span>
<span data-ttu-id="ee19e-148">Hallo SDK omvat Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="ee19e-148">hello SDK includes hello following items:</span></span>

* <span data-ttu-id="ee19e-149">**LEESMIJ**.</span><span class="sxs-lookup"><span data-stu-id="ee19e-149">**README**.</span></span> <span data-ttu-id="ee19e-150">Legt uit hoe toouse multi-factor Authentication-API's in een nieuwe of bestaande toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="ee19e-150">Explains how toouse hello Multi-Factor Authentication APIs in a new or existing application.</span></span>
* <span data-ttu-id="ee19e-151">**Bronbestanden** voor multi-factor Authentication</span><span class="sxs-lookup"><span data-stu-id="ee19e-151">**Source files** for Multi-Factor Authentication</span></span>
* <span data-ttu-id="ee19e-152">**Clientcertificaat** dat u toocommunicate Hello multi-factor Authentication-service</span><span class="sxs-lookup"><span data-stu-id="ee19e-152">**Client certificate** that you use toocommunicate with hello Multi-Factor Authentication service</span></span>
* <span data-ttu-id="ee19e-153">**Persoonlijke sleutel** voor Hallo certificaat</span><span class="sxs-lookup"><span data-stu-id="ee19e-153">**Private key** for hello certificate</span></span>
* <span data-ttu-id="ee19e-154">**Aanroepen van resultaten.**</span><span class="sxs-lookup"><span data-stu-id="ee19e-154">**Call results.**</span></span> <span data-ttu-id="ee19e-155">Een lijst met oproepresultaatcodes.</span><span class="sxs-lookup"><span data-stu-id="ee19e-155">A list of call result codes.</span></span> <span data-ttu-id="ee19e-156">tooopen dit bestand, gebruikt u een toepassing met de tekst, zoals WordPad.</span><span class="sxs-lookup"><span data-stu-id="ee19e-156">tooopen this file, use an application with text formatting, such as WordPad.</span></span> <span data-ttu-id="ee19e-157">Gebruik Hallo resultaat codes tootest aanroepen en problemen oplossen Hallo-implementatie van multi-factor Authentication in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="ee19e-157">Use hello call result codes tootest and troubleshoot hello implementation of Multi-Factor Authentication in your application.</span></span> <span data-ttu-id="ee19e-158">Ze zijn geen statuscodes voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="ee19e-158">They are not authentication status codes.</span></span>
* <span data-ttu-id="ee19e-159">**Voorbeelden.**</span><span class="sxs-lookup"><span data-stu-id="ee19e-159">**Examples.**</span></span> <span data-ttu-id="ee19e-160">Voorbeeldcode voor een eenvoudige werkende implementatie van multi-factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="ee19e-160">Sample code for a basic working implementation of Multi-Factor Authentication.</span></span>

> [!WARNING]
> <span data-ttu-id="ee19e-161">Hallo-clientcertificaat is een unieke persoonlijk certificaat die speciaal voor u is gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="ee19e-161">hello client certificate is a unique private certificate that was generated especially for you.</span></span> <span data-ttu-id="ee19e-162">Geen delen of dit bestand verloren.</span><span class="sxs-lookup"><span data-stu-id="ee19e-162">Do not share or lose this file.</span></span> <span data-ttu-id="ee19e-163">Het is de beveiliging van uw belangrijkste tooensuring Hallo van uw communicatie met Hallo multi-factor Authentication-service.</span><span class="sxs-lookup"><span data-stu-id="ee19e-163">It’s your key tooensuring hello security of your communications with hello Multi-Factor Authentication service.</span></span>

## <a name="code-sample"></a><span data-ttu-id="ee19e-164">Codevoorbeeld</span><span class="sxs-lookup"><span data-stu-id="ee19e-164">Code sample</span></span>
<span data-ttu-id="ee19e-165">Dit voorbeeld laat zien u hoe toouse Hallo API's in de SDK van Azure multi-factor Authentication tooadd standaardmodus stem Hallo verificatie tooyour toepassing aanroepen.</span><span class="sxs-lookup"><span data-stu-id="ee19e-165">This code sample shows you how toouse hello APIs in hello Azure Multi-Factor Authentication SDK tooadd standard mode voice call verification tooyour application.</span></span> <span data-ttu-id="ee19e-166">Standaardmodus is een telefoongesprek die Hallo gebruiker reageert tooby Hallo # te drukken.</span><span class="sxs-lookup"><span data-stu-id="ee19e-166">Standard mode is a telephone call that hello user responds tooby pressing hello # key.</span></span>

<span data-ttu-id="ee19e-167">In dit voorbeeld Hallo C# .NET 2.0 SDK multi-factor Authentication in een eenvoudige ASP.NET-toepassing met C#-serverzijde logica gebruikt, maar gaat Hallo op dezelfde manier in andere talen.</span><span class="sxs-lookup"><span data-stu-id="ee19e-167">This example uses hello C# .NET 2.0 Multi-Factor Authentication SDK in a basic ASP.NET application with C# server-side logic, but hello process is similar in other languages.</span></span> <span data-ttu-id="ee19e-168">Omdat Hallo SDK bronbestanden, niet-uitvoerbare bestanden bevat, kunt u Hallo-bestanden maken en ernaar te verwijzen of opnemen rechtstreeks in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="ee19e-168">Because hello SDK includes source files, not executable files, you can build hello files and reference them or include them directly in your application.</span></span>

> [!NOTE]
> <span data-ttu-id="ee19e-169">Bij het implementeren van multi-factor Authentication gebruiken Hallo aanvullende methoden (telefoongesprek of tekstbericht) als secundair of tertiair verificatie toosupplement primaire authenticatiemethode (gebruikersnaam en wachtwoord).</span><span class="sxs-lookup"><span data-stu-id="ee19e-169">When implementing Multi-Factor Authentication, use hello additional methods (phone call or text message) as secondary or tertiary verification toosupplement your primary authentication method (username and password).</span></span> <span data-ttu-id="ee19e-170">Deze methoden zijn niet bedoeld als primaire verificatiemethoden.</span><span class="sxs-lookup"><span data-stu-id="ee19e-170">These methods are not designed as primary authentication methods.</span></span>

### <a name="code-sample-overview"></a><span data-ttu-id="ee19e-171">Overzicht van de code-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="ee19e-171">Code Sample Overview</span></span>
<span data-ttu-id="ee19e-172">Deze voorbeeldcode voor een eenvoudige demo webtoepassing maakt gebruik van een telefoongesprek met een # reactie tooverify Hallo gebruikersverificatie.</span><span class="sxs-lookup"><span data-stu-id="ee19e-172">This sample code for a simple web demo application uses a telephone call with a # key response tooverify hello user's authentication.</span></span> <span data-ttu-id="ee19e-173">Deze factoren telefoongesprek wordt genoemd in de multi-factor Authentication standaardmodus.</span><span class="sxs-lookup"><span data-stu-id="ee19e-173">This telephone call factor is known in Multi-Factor Authentication as standard mode.</span></span>

<span data-ttu-id="ee19e-174">Hallo clientcode omvat niet alle multi-factor Authentication-specifieke elementen bevat.</span><span class="sxs-lookup"><span data-stu-id="ee19e-174">hello client-side code does not include any Multi-Factor Authentication-specific elements.</span></span> <span data-ttu-id="ee19e-175">Omdat de aanvullende verificatiefactoren Hallo onafhankelijk van de primaire verificatie hello, kunt u ze kunt toevoegen zonder bestaande Hallo aanmelding interface.</span><span class="sxs-lookup"><span data-stu-id="ee19e-175">Because hello additional authentication factors are independent of hello primary authentication, you can add them without changing hello existing sign-on interface.</span></span> <span data-ttu-id="ee19e-176">Hallo API's in Hallo multi-factor-SDK kunt u Hallo gebruikerservaring aanpassen, maar hoeft u mogelijk niet toochange iets helemaal.</span><span class="sxs-lookup"><span data-stu-id="ee19e-176">hello APIs in hello Multi-Factor SDK let you customize hello user experience, but you might not need toochange anything at all.</span></span>

<span data-ttu-id="ee19e-177">Hallo servercode wordt standaard verificatiemodus toegevoegd in stap 2.</span><span class="sxs-lookup"><span data-stu-id="ee19e-177">hello server-side code adds standard-mode authentication in Step 2.</span></span> <span data-ttu-id="ee19e-178">Er wordt een PfAuthParams-object gemaakt met Hallo-parameters die vereist voor de verificatie standaardmodus zijn: gebruikersnaam, telefoon aantal en de modus en Hallo pad toohello clientcertificaat (CertFilePath), die is in elke aanroep vereist.</span><span class="sxs-lookup"><span data-stu-id="ee19e-178">It creates a PfAuthParams object with hello parameters that are required for standard-mode verification: username, telephone number, and mode, and hello path toohello client certificate (CertFilePath), which is required in each call.</span></span> <span data-ttu-id="ee19e-179">Zie voor een demonstratie van alle parameters in PfAuthParams Hallo voorbeeld van een bestand in Hallo SDK.</span><span class="sxs-lookup"><span data-stu-id="ee19e-179">For a demonstration of all parameters in PfAuthParams, see hello Example file in hello SDK.</span></span>

<span data-ttu-id="ee19e-180">Hallo-code wordt vervolgens Hallo PfAuthParams object toohello pf_authenticate() functie doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="ee19e-180">Next, hello code passes hello PfAuthParams object toohello pf_authenticate() function.</span></span> <span data-ttu-id="ee19e-181">Hallo-retourwaarde geeft Hallo slagen of mislukken van Hallo-verificatie.</span><span class="sxs-lookup"><span data-stu-id="ee19e-181">hello return value indicates hello success or failure of hello authentication.</span></span> <span data-ttu-id="ee19e-182">Hallo-parameters, callStatus en Aanroepstatus, extra aanroep resultaat informatie bevatten.</span><span class="sxs-lookup"><span data-stu-id="ee19e-182">hello out parameters, callStatus, and errorID, contain additional call result information.</span></span> <span data-ttu-id="ee19e-183">oproepresultaatcodes Hello zijn gedocumenteerd in Hallo aanroep resultatenbestand in Hallo SDK.</span><span class="sxs-lookup"><span data-stu-id="ee19e-183">hello call result codes are documented in hello call results file in hello SDK.</span></span>

<span data-ttu-id="ee19e-184">Deze minimale implementatie kan worden geschreven in een paar regels.</span><span class="sxs-lookup"><span data-stu-id="ee19e-184">This minimal implementation can be written in a few lines.</span></span> <span data-ttu-id="ee19e-185">In productiecode moet zou u bevatten echter meer geavanceerde foutafhandeling, extra databasecode en een betere gebruikerservaring.</span><span class="sxs-lookup"><span data-stu-id="ee19e-185">However, in production code, you would include more sophisticated error handling, additional database code, and an enhanced user experience.</span></span>

### <a name="web-client-code"></a><span data-ttu-id="ee19e-186">Web-Client-Code</span><span class="sxs-lookup"><span data-stu-id="ee19e-186">Web Client Code</span></span>
<span data-ttu-id="ee19e-187">Hallo volgt web clientcode voor een demo-pagina.</span><span class="sxs-lookup"><span data-stu-id="ee19e-187">hello following is web client code for a demo page.</span></span>

    <%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="\_Default" %>

    <!DOCTYPE html>

    <html xmlns="http://www.w3.org/1999/xhtml">
    <head runat="server">
    <title>Multi-Factor Authentication Demo</title>
    </head>
    <body>
    <h1>Azure Multi-Factor Authentication Demo</h1>
    <form id="form1" runat="server">

    <div style="width:auto; float:left">
    Username:&nbsp;<br />
    Password:&nbsp;<br />
    </div>

    <div">
    <asp:TextBox id="username" runat="server" width="100px"/><br />
    <asp:Textbox id="password" runat="server" width="100px" TextMode="password" /><br />
    </div>

    <asp:Button id="btnSubmit" runat="server" Text="Log in" onClick="btnSubmit_Click"/>

    <p><asp:Label ID="lblResult" runat="server"></asp:Label></p>

    </form>
    </body>
    </html>


### <a name="server-side-code"></a><span data-ttu-id="ee19e-188">Code op de server</span><span class="sxs-lookup"><span data-stu-id="ee19e-188">Server-Side Code</span></span>
<span data-ttu-id="ee19e-189">Multi-factor Authentication is geconfigureerd en worden uitgevoerd in stap 2 in Hallo servercode te volgen.</span><span class="sxs-lookup"><span data-stu-id="ee19e-189">In hello following server-side code, Multi-Factor Authentication is configured and run in Step 2.</span></span> <span data-ttu-id="ee19e-190">Standaard-modus (MODE_STANDARD) is dat een telefoongesprek toowhich Hallo gebruiker reageert door Hallo #-toets te drukken.</span><span class="sxs-lookup"><span data-stu-id="ee19e-190">Standard mode (MODE_STANDARD) is a telephone call toowhich hello user responds by pressing hello # key.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.Web.UI;
    using System.Web.UI.WebControls;

    public partial class \_Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
        }

        protected void btnSubmit_Click(object sender, EventArgs e)
        {
            // Step 1: Validate hello username and password
            if (username.Text != "Contoso" || password.Text != "password")
            {
                lblResult.ForeColor = System.Drawing.Color.Red;
                lblResult.Text = "Username or password incorrect.";
            }
            else
            {
                // Step 2: Perform multi-factor authentication

                // Add call details from hello user database.
                PfAuthParams pfAuthParams = new PfAuthParams();
                pfAuthParams.Username = username.Text;
                pfAuthParams.Phone = "5555555555";
                pfAuthParams.Mode = pf_auth.MODE_STANDARD;

                // Specify a client certificate
                // NOTE: This file contains hello private key for hello client
                // certificate. It must be stored with appropriate file
                // permissions.
                pfAuthParams.CertFilePath = "c:\\cert_key.p12";

                // Perform phone-based authentication
                int callStatus;
                int errorId;

                if(pf_auth.pf_authenticate(pfAuthParams, out callStatus, out errorId))
                {
                    lblResult.ForeColor = System.Drawing.Color.Green;
                    lblResult.Text = "Multi-Factor Authentication succeeded.";
                }
                else
                {
                    lblResult.ForeColor = System.Drawing.Color.Red;
                    lblResult.Text = "Multi-Factor Authentication failed.";
                }
            }

        }
    }
