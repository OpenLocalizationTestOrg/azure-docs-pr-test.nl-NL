---
title: aaaAzure AD v2 JS SPA begeleide Setup - configureren (ARP) | Microsoft Docs
description: Hoe een API waarvoor toegangstokens door Azure Active Directory v2-eindpunt (ARP) kunnen aanroepen in JavaScript SPA-toepassingen
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
ms.openlocfilehash: 157f4e342cd684294e24da6ee1fad8a7c2fc266a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a><span data-ttu-id="39ea5-103">Toevoegen van de toepassing hello registratie informatie tooyour App</span><span class="sxs-lookup"><span data-stu-id="39ea5-103">Add hello application’s registration information tooyour App</span></span>

<span data-ttu-id="39ea5-104">In deze stap maakt u moet tooconfigure Hallo Omleidings-URL van de registratiegegevens van de toepassing en voeg vervolgens Hallo toepassings-Id tooyour JavaScript SPA-toepassing.</span><span class="sxs-lookup"><span data-stu-id="39ea5-104">In this step, you need tooconfigure hello Redirect URL of your application registration information and then add hello Application Id tooyour JavaScript SPA application.</span></span>

### <a name="configure-redirect-url"></a><span data-ttu-id="39ea5-105">Omleidings-URL configureren</span><span class="sxs-lookup"><span data-stu-id="39ea5-105">Configure redirect URL</span></span>

<span data-ttu-id="39ea5-106">Hallo configureren `Redirect URL` veld hierboven met Hallo-URL voor uw pagina index.html op basis van uw webserver en klik vervolgens op *Update*.</span><span class="sxs-lookup"><span data-stu-id="39ea5-106">Configure hello `Redirect URL` field above with hello URL for your index.html page based on your web server, then click *Update*.</span></span>


> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a><span data-ttu-id="39ea5-107">Visual Studio-instructies voor het verkrijgen van de omleidings-URL</span><span class="sxs-lookup"><span data-stu-id="39ea5-107">Visual Studio instructions for obtaining redirect URL</span></span>
> <span data-ttu-id="39ea5-108">tooobtain uw Omleidings-URL, volg de instructies van de Hallo is hieronder:</span><span class="sxs-lookup"><span data-stu-id="39ea5-108">tooobtain your redirect URL, follow hello instructions below:</span></span>
> 1.    <span data-ttu-id="39ea5-109">In *Solution Explorer*, selecteer Hallo-project en bekijkt hello `Properties` venster (als u een venster met eigenschappen niet ziet, drukt u op `F4`)</span><span class="sxs-lookup"><span data-stu-id="39ea5-109">In *Solution Explorer*, select hello project and look at hello `Properties` window (if you don’t see a Properties window, press `F4`)</span></span>
> 2.    <span data-ttu-id="39ea5-110">Hallo-waarde van kopiëren `URL` toohello Klembord:</span><span class="sxs-lookup"><span data-stu-id="39ea5-110">Copy hello value from `URL` toohello clipboard:</span></span><br/> <span data-ttu-id="39ea5-111">![Projecteigenschappen](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span><span class="sxs-lookup"><span data-stu-id="39ea5-111">![Project properties](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span></span><br />
> 3.    <span data-ttu-id="39ea5-112">Plak Hallo-waarde als een `Redirect URL` op Hallo boven aan deze pagina, klik vervolgens op`Update`</span><span class="sxs-lookup"><span data-stu-id="39ea5-112">Paste hello value as a `Redirect URL` on hello top of this page, then click `Update`</span></span>

<p/>

> #### <a name="setting-redirect-url-for-python"></a><span data-ttu-id="39ea5-113">Instelling Omleidings-URL voor Python</span><span class="sxs-lookup"><span data-stu-id="39ea5-113">Setting Redirect URL for Python</span></span>
> <span data-ttu-id="39ea5-114">Voor Python, kunt u de poort van de webserver Hallo via de opdrachtregel instellen.</span><span class="sxs-lookup"><span data-stu-id="39ea5-114">For Python, you can set hello web server port via command line.</span></span> <span data-ttu-id="39ea5-115">Deze Begeleide installatie Hallo poort 8080 gebruikt ter referentie, maar kunt u gratis toouse een willekeurige poort beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="39ea5-115">This guided setup uses hello port 8080 for reference but feel free toouse any other port available.</span></span> <span data-ttu-id="39ea5-116">In elk geval Volg onderstaande tooset van een Omleidings-URL in inschrijvingsgegevens Hallo-toepassing hello instructies:</span><span class="sxs-lookup"><span data-stu-id="39ea5-116">In any case, follow hello instructions below tooset up a redirect URL in hello application registration information:</span></span><br/>
> <span data-ttu-id="39ea5-117">Stel `http://localhost:8080/` als een `Redirect URL` op Hallo boven aan deze pagina, of gebruik `http://localhost:[port]/` als u een aangepaste TCP-poort (waar *[poort]* Hallo aangepaste TCP-poortnummer is), en klik op 'Bijwerken'</span><span class="sxs-lookup"><span data-stu-id="39ea5-117">Set `http://localhost:8080/` as a `Redirect URL` on hello top of this page, or use `http://localhost:[port]/` if you are using a custom TCP port (where *[port]* is hello custom TCP port number), and then click 'Update'</span></span>

### <a name="configure-your-javascript-spa-application"></a><span data-ttu-id="39ea5-118">Uw toepassing JavaScript SPA configureren</span><span class="sxs-lookup"><span data-stu-id="39ea5-118">Configure your JavaScript SPA application</span></span>

1.  <span data-ttu-id="39ea5-119">Maak een bestand met de naam `msalconfig.js` met registratiegegevens Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="39ea5-119">Create a file named `msalconfig.js` containing hello application registration information.</span></span> <span data-ttu-id="39ea5-120">Als u Visual Studio, selecteer Hallo-project (project basismap), klik met de rechtermuisknop en selecteer: `Add`  >  `New Item`  >  `JavaScript File`.</span><span class="sxs-lookup"><span data-stu-id="39ea5-120">If you are using Visual Studio, select hello project (project root folder), right-click and select: `Add` > `New Item` > `JavaScript File`.</span></span> <span data-ttu-id="39ea5-121">Geef deze de naam`msalconfig.js`</span><span class="sxs-lookup"><span data-stu-id="39ea5-121">Name it `msalconfig.js`</span></span>
2.  <span data-ttu-id="39ea5-122">Hallo na code tooyour toevoegen `msalconfig.js` bestand:</span><span class="sxs-lookup"><span data-stu-id="39ea5-122">Add hello following code tooyour `msalconfig.js` file:</span></span>

```javascript
var msalconfig = {
    clientID: "[Enter hello application Id here]",
    redirectUri: location.origin
};
``` 
