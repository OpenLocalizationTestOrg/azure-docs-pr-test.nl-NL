---
title: aaaAzure AD v2 JS SPA begeleide Setup - configureren | Microsoft Docs
description: Hoe een API waarvoor toegangstokens door Azure Active Directory-v2-eindpunt kunnen aanroepen in JavaScript SPA-toepassingen
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 1b93298d4bd4e17dd261dbb75502a122c30aac97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="register-your-application"></a><span data-ttu-id="170e6-103">Uw toepassing registreren</span><span class="sxs-lookup"><span data-stu-id="170e6-103">Register your application</span></span>

<span data-ttu-id="170e6-104">Er zijn meerdere manieren toocreate een toepassing, selecteer een van beide:</span><span class="sxs-lookup"><span data-stu-id="170e6-104">There are multiple ways toocreate an application, please select one of them:</span></span>

### <a name="option-1-register-your-application-express-mode"></a><span data-ttu-id="170e6-105">Optie 1: De toepassing (Express-modus) registreren</span><span class="sxs-lookup"><span data-stu-id="170e6-105">Option 1: Register your application (Express mode)</span></span>
<span data-ttu-id="170e6-106">Nu u uw toepassing in Hallo tooregister moet *Portal voor registratie van Microsoft-toepassing*:</span><span class="sxs-lookup"><span data-stu-id="170e6-106">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>

1.  <span data-ttu-id="170e6-107">Registreren van uw toepassing via Hallo [Portal voor registratie van Microsoft-toepassing](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)</span><span class="sxs-lookup"><span data-stu-id="170e6-107">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)</span></span>
2.  <span data-ttu-id="170e6-108">Voer een naam voor uw toepassing en uw e-mailadres</span><span class="sxs-lookup"><span data-stu-id="170e6-108">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="170e6-109">Zorg ervoor Hallo-optie voor *Begeleide instelprocedure* is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="170e6-109">Make sure hello option for *Guided Setup* is checked</span></span>
4.  <span data-ttu-id="170e6-110">Ga als volgt Hallo instructies tooobtain Hallo toepassings-ID en plak deze in uw code</span><span class="sxs-lookup"><span data-stu-id="170e6-110">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="option-2-register-your-application-advanced-mode"></a><span data-ttu-id="170e6-111">Optie 2: De toepassing (geavanceerde modus) registreren</span><span class="sxs-lookup"><span data-stu-id="170e6-111">Option 2: Register your application (Advanced mode)</span></span>

1. <span data-ttu-id="170e6-112">Ga toohello [Portal voor registratie van Microsoft-toepassing](https://apps.dev.microsoft.com/portal/register-app) tooregister een toepassing</span><span class="sxs-lookup"><span data-stu-id="170e6-112">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="170e6-113">Voer een naam voor uw toepassing en uw e-mailadres</span><span class="sxs-lookup"><span data-stu-id="170e6-113">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="170e6-114">Zorg ervoor Hallo-optie voor *Begeleide instelprocedure* is uitgeschakeld</span><span class="sxs-lookup"><span data-stu-id="170e6-114">Make sure hello option for *Guided Setup* is unchecked</span></span>
4.  <span data-ttu-id="170e6-115">Klik op `Add Platform`, selecteer vervolgens`Web`</span><span class="sxs-lookup"><span data-stu-id="170e6-115">Click `Add Platform`, then select `Web`</span></span>
5. <span data-ttu-id="170e6-116">Hallo toevoegen `Redirect URL` die overeenkomen met de URL van de van toohello toepassing is op basis van uw webserver.</span><span class="sxs-lookup"><span data-stu-id="170e6-116">Add hello `Redirect URL` that correspond toohello application's URL based on your web server.</span></span> <span data-ttu-id="170e6-117">Zie Hallo secties voor instructies over het tooset / verkrijgen Hallo Omleidings-URL in Visual Studio en Python.</span><span class="sxs-lookup"><span data-stu-id="170e6-117">See hello sections below for instructions on how tooset/ obtain hello redirect URL in Visual Studio and Python.</span></span>
6. <span data-ttu-id="170e6-118">Klik op *opslaan*</span><span class="sxs-lookup"><span data-stu-id="170e6-118">Click *Save*</span></span>

> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a><span data-ttu-id="170e6-119">Visual Studio-instructies voor het verkrijgen van de omleidings-URL</span><span class="sxs-lookup"><span data-stu-id="170e6-119">Visual Studio instructions for obtaining redirect URL</span></span>
> <span data-ttu-id="170e6-120">Ga als volgt Hallo instructies tooobtain Omleidings-URL:</span><span class="sxs-lookup"><span data-stu-id="170e6-120">Follow hello instructions tooobtain your redirect URL:</span></span>
> 1.    <span data-ttu-id="170e6-121">In *Solution Explorer*, selecteer Hallo-project en bekijkt hello `Properties` venster (als u een venster met eigenschappen niet ziet, drukt u op `F4`)</span><span class="sxs-lookup"><span data-stu-id="170e6-121">In *Solution Explorer*, select hello project and look at hello `Properties` window (if you don’t see a Properties window, press `F4`)</span></span>
> 2.    <span data-ttu-id="170e6-122">Hallo-waarde van kopiëren `URL` toohello Klembord:</span><span class="sxs-lookup"><span data-stu-id="170e6-122">Copy hello value from `URL` toohello clipboard:</span></span><br/> <span data-ttu-id="170e6-123">![Projecteigenschappen](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span><span class="sxs-lookup"><span data-stu-id="170e6-123">![Project properties](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span></span><br />
> 3.    <span data-ttu-id="170e6-124">Overschakelen back toohello *toepassing Registratieportal* en plak Hallo-waarde als een `Redirect URL` en klik op 'Opslaan'</span><span class="sxs-lookup"><span data-stu-id="170e6-124">Switch back toohello *Application Registration Portal* and paste hello value as a `Redirect URL` and click 'Save'</span></span>

<p/>

> #### <a name="setting-redirect-url-for-python"></a><span data-ttu-id="170e6-125">Instelling Omleidings-URL voor Python</span><span class="sxs-lookup"><span data-stu-id="170e6-125">Setting Redirect URL for Python</span></span>
> <span data-ttu-id="170e6-126">Voor Python, kunt u de poort van de webserver Hallo via de opdrachtregel instellen.</span><span class="sxs-lookup"><span data-stu-id="170e6-126">For Python, you can set hello web server port via command line.</span></span> <span data-ttu-id="170e6-127">Deze Begeleide installatie Hallo poort 8080 gebruikt ter referentie, maar kunt u gratis toouse een willekeurige poort beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="170e6-127">This guided setup uses hello port 8080 for reference but feel free toouse any other port available.</span></span> <span data-ttu-id="170e6-128">In elk geval Volg onderstaande tooset van een Omleidings-URL in inschrijvingsgegevens Hallo-toepassing hello instructies:</span><span class="sxs-lookup"><span data-stu-id="170e6-128">In any case, follow hello instructions below tooset up a redirect URL in hello application registration information:</span></span><br/>
> - <span data-ttu-id="170e6-129">Overschakelen back toohello *Portal voor registratie van toepassing* en stel `http://localhost:8080/` als een `Redirect URL`, of gebruik `http://localhost:[port]/` als u een aangepaste TCP-poort (waarbij *[poort]* Hallo aangepaste TCP-poort getal) en klik op 'Opslaan'</span><span class="sxs-lookup"><span data-stu-id="170e6-129">Switch back toohello *Application Registration Portal* and set `http://localhost:8080/` as a `Redirect URL`, or use `http://localhost:[port]/` if you are using a custom TCP port (where *[port]* is hello custom TCP port number) and click 'Save'</span></span>


#### <a name="configure-your-javascript-spa"></a><span data-ttu-id="170e6-130">Uw JavaScript SPA configureren</span><span class="sxs-lookup"><span data-stu-id="170e6-130">Configure your JavaScript SPA</span></span>

1.  <span data-ttu-id="170e6-131">Maak een bestand met de naam `msalconfig.js` met registratiegegevens Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="170e6-131">Create a file named `msalconfig.js` containing hello application registration information.</span></span> <span data-ttu-id="170e6-132">Als u Visual Studio, selecteer Hallo-project (project basismap), klik met de rechtermuisknop en selecteer: `Add`  >  `New Item`  >  `JavaScript File`.</span><span class="sxs-lookup"><span data-stu-id="170e6-132">If you are using Visual Studio, select hello project (project root folder), right-click and select: `Add` > `New Item` > `JavaScript File`.</span></span> <span data-ttu-id="170e6-133">Geef deze de naam`msalconfig.js`</span><span class="sxs-lookup"><span data-stu-id="170e6-133">Name it `msalconfig.js`</span></span>
2.  <span data-ttu-id="170e6-134">Hallo na code tooyour toevoegen `msalconfig.js` bestand:</span><span class="sxs-lookup"><span data-stu-id="170e6-134">Add hello following code tooyour `msalconfig.js` file:</span></span>

```javascript
var msalconfig = {
    clientID: "Enter_the_Application_Id_here",
    redirectUri: location.origin
};
```
<ol start="3">
<li>
<span data-ttu-id="170e6-135">Vervang <code>Enter_the_Application_Id_here</code> Hello toepassings-Id die u zojuist hebt geregistreerd</span><span class="sxs-lookup"><span data-stu-id="170e6-135">Replace <code>Enter_the_Application_Id_here</code> with hello Application Id you just registered</span></span>
</li>
</ol>
