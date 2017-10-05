---
title: Azure AD v2 JS SPA begeleide Setup - configureren (ARP) | Microsoft Docs
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
ms.openlocfilehash: 708f4ff606d79639de979918a9cacd4ed75db311
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
## <a name="add-the-applications-registration-information-to-your-app"></a><span data-ttu-id="0b344-103">De registratiegegevens van de toepassing toevoegen aan uw App</span><span class="sxs-lookup"><span data-stu-id="0b344-103">Add the application’s registration information to your App</span></span>

<span data-ttu-id="0b344-104">In deze stap moet u de omleidings-URL van de registratiegegevens van de toepassing configureren en vervolgens de toepassings-Id toe te voegen aan uw toepassing JavaScript SPA.</span><span class="sxs-lookup"><span data-stu-id="0b344-104">In this step, you need to configure the Redirect URL of your application registration information and then add the Application Id to your JavaScript SPA application.</span></span>

### <a name="configure-redirect-url"></a><span data-ttu-id="0b344-105">Omleidings-URL configureren</span><span class="sxs-lookup"><span data-stu-id="0b344-105">Configure redirect URL</span></span>

<span data-ttu-id="0b344-106">Configureer de `Redirect URL` veld boven aan de URL voor uw pagina index.html op basis van uw webserver en klik vervolgens op *Update*.</span><span class="sxs-lookup"><span data-stu-id="0b344-106">Configure the `Redirect URL` field above with the URL for your index.html page based on your web server, then click *Update*.</span></span>


> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a><span data-ttu-id="0b344-107">Visual Studio-instructies voor het verkrijgen van de omleidings-URL</span><span class="sxs-lookup"><span data-stu-id="0b344-107">Visual Studio instructions for obtaining redirect URL</span></span>
> <span data-ttu-id="0b344-108">Als u de omleidings-URL, volgt u onderstaande instructies:</span><span class="sxs-lookup"><span data-stu-id="0b344-108">To obtain your redirect URL, follow the instructions below:</span></span>
> 1.    <span data-ttu-id="0b344-109">In *Solution Explorer*, selecteert u het project en bekijk de `Properties` venster (als u een venster met eigenschappen niet ziet, drukt u op `F4`)</span><span class="sxs-lookup"><span data-stu-id="0b344-109">In *Solution Explorer*, select the project and look at the `Properties` window (if you don’t see a Properties window, press `F4`)</span></span>
> 2.    <span data-ttu-id="0b344-110">Kopieer de waarde van `URL` naar het Klembord:</span><span class="sxs-lookup"><span data-stu-id="0b344-110">Copy the value from `URL` to the clipboard:</span></span><br/> <span data-ttu-id="0b344-111">![Projecteigenschappen](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span><span class="sxs-lookup"><span data-stu-id="0b344-111">![Project properties](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span></span><br />
> 3.    <span data-ttu-id="0b344-112">Plak de waarde als een `Redirect URL` Klik boven aan deze pagina`Update`</span><span class="sxs-lookup"><span data-stu-id="0b344-112">Paste the value as a `Redirect URL` on the top of this page, then click `Update`</span></span>

<p/>

> #### <a name="setting-redirect-url-for-python"></a><span data-ttu-id="0b344-113">Instelling Omleidings-URL voor Python</span><span class="sxs-lookup"><span data-stu-id="0b344-113">Setting Redirect URL for Python</span></span>
> <span data-ttu-id="0b344-114">Voor Python, kunt u de web server-poort via de opdrachtregel instellen.</span><span class="sxs-lookup"><span data-stu-id="0b344-114">For Python, you can set the web server port via command line.</span></span> <span data-ttu-id="0b344-115">Deze begeleide setup gebruikt de poort 8080 voor verwijzing, maar gerust om andere poort beschikbaar te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0b344-115">This guided setup uses the port 8080 for reference but feel free to use any other port available.</span></span> <span data-ttu-id="0b344-116">In elk geval Volg de onderstaande instructies voor het instellen van een Omleidings-URL in de registratiegegevens van toepassing:</span><span class="sxs-lookup"><span data-stu-id="0b344-116">In any case, follow the instructions below to set up a redirect URL in the application registration information:</span></span><br/>
> <span data-ttu-id="0b344-117">Stel `http://localhost:8080/` als een `Redirect URL` boven aan deze pagina of gebruik `http://localhost:[port]/` als u een aangepaste TCP-poort (waar *[poort]* het aangepaste TCP-poortnummer), en klik op 'Bijwerken'</span><span class="sxs-lookup"><span data-stu-id="0b344-117">Set `http://localhost:8080/` as a `Redirect URL` on the top of this page, or use `http://localhost:[port]/` if you are using a custom TCP port (where *[port]* is the custom TCP port number), and then click 'Update'</span></span>

### <a name="configure-your-javascript-spa-application"></a><span data-ttu-id="0b344-118">Uw toepassing JavaScript SPA configureren</span><span class="sxs-lookup"><span data-stu-id="0b344-118">Configure your JavaScript SPA application</span></span>

1.  <span data-ttu-id="0b344-119">Maak een bestand met de naam `msalconfig.js` met de registratiegegevens van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="0b344-119">Create a file named `msalconfig.js` containing the application registration information.</span></span> <span data-ttu-id="0b344-120">Als u Visual Studio gebruikt, selecteert u het project (basismap project), klik met de rechtermuisknop en selecteer: `Add`  >  `New Item`  >  `JavaScript File`.</span><span class="sxs-lookup"><span data-stu-id="0b344-120">If you are using Visual Studio, select the project (project root folder), right-click and select: `Add` > `New Item` > `JavaScript File`.</span></span> <span data-ttu-id="0b344-121">Geef deze de naam`msalconfig.js`</span><span class="sxs-lookup"><span data-stu-id="0b344-121">Name it `msalconfig.js`</span></span>
2.  <span data-ttu-id="0b344-122">Voeg de volgende code naar uw `msalconfig.js` bestand:</span><span class="sxs-lookup"><span data-stu-id="0b344-122">Add the following code to your `msalconfig.js` file:</span></span>

```javascript
var msalconfig = {
    clientID: "[Enter the application Id here]",
    redirectUri: location.origin
};
``` 
