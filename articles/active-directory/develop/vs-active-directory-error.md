---
title: aaaHow toodiagnose fouten Hello Wizard van Azure Active Directory-verbinding
description: wizard Hallo active directory-verbinding een incompatibel verificatietype gedetecteerd
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: dd89ea63-4e45-4da1-9642-645b9309670a
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/05/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: f71c5b41457c0c8db05042e8d5f723e58ad11844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="diagnosing-errors-with-hello-azure-active-directory-connection-wizard"></a><span data-ttu-id="a3d79-103">Oplossen van problemen met Hallo Wizard van Azure Active Directory-verbinding</span><span class="sxs-lookup"><span data-stu-id="a3d79-103">Diagnosing errors with hello Azure Active Directory Connection Wizard</span></span>
<span data-ttu-id="a3d79-104">Hallo wizard gedetecteerd tijdens het detecteren van eerdere verificatiecode op te geven, een incompatibel verificatietype.</span><span class="sxs-lookup"><span data-stu-id="a3d79-104">While detecting previous authentication code, hello wizard detected an incompatible authentication type.</span></span>   

## <a name="what-is-being-checked"></a><span data-ttu-id="a3d79-105">Wat wordt gecontroleerd?</span><span class="sxs-lookup"><span data-stu-id="a3d79-105">What is being checked?</span></span>
<span data-ttu-id="a3d79-106">**Opmerking:** toocorrectly vorige verificatiecode op te geven in een project detecteren, Hallo project moet worden gebouwd.</span><span class="sxs-lookup"><span data-stu-id="a3d79-106">**Note:** toocorrectly detect previous authentication code in a project, hello project must be built.</span></span>  <span data-ttu-id="a3d79-107">Als u deze fout is opgetreden en er geen een vorige verificatiecode op te geven in uw project, opnieuw en probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="a3d79-107">If you encountered this error and you don't have a previous authentication code in your project, rebuild and try again.</span></span>

### <a name="project-types"></a><span data-ttu-id="a3d79-108">Projecttypen</span><span class="sxs-lookup"><span data-stu-id="a3d79-108">Project Types</span></span>
<span data-ttu-id="a3d79-109">Hallo wizard controleert Hallo type project dat u ontwikkelt zodat deze Hallo rechts verificatielogica Hallo-project injecteren kan.</span><span class="sxs-lookup"><span data-stu-id="a3d79-109">hello wizard checks hello type of project you’re developing so it can inject hello right authentication logic into hello project.</span></span>  <span data-ttu-id="a3d79-110">Als er domeincontroller die is afgeleid van `ApiController` in project Hallo Hallo-project wordt beschouwd als een WebAPI-project.</span><span class="sxs-lookup"><span data-stu-id="a3d79-110">If there is any controller that derives from `ApiController` in hello project, hello project is considered a WebAPI project.</span></span>  <span data-ttu-id="a3d79-111">Als er alleen domeincontrollers die zijn afgeleid van `MVC.Controller` in project Hallo Hallo-project wordt beschouwd als een MVC-project.</span><span class="sxs-lookup"><span data-stu-id="a3d79-111">If there are only controllers that derive from `MVC.Controller` in hello project, hello project is considered an MVC project.</span></span>  <span data-ttu-id="a3d79-112">Overige wordt niet ondersteund door de wizard Hallo.</span><span class="sxs-lookup"><span data-stu-id="a3d79-112">Anything else is not supported by hello wizard.</span></span>

### <a name="compatible-authentication-code"></a><span data-ttu-id="a3d79-113">Compatibel verificatiecode op te geven</span><span class="sxs-lookup"><span data-stu-id="a3d79-113">Compatible Authentication Code</span></span>
<span data-ttu-id="a3d79-114">Hallo wizard controleert ook of de verificatie-instellingen die eerder zijn geconfigureerd met de wizard Hallo of compatibel zijn met het Hallo-wizard.</span><span class="sxs-lookup"><span data-stu-id="a3d79-114">hello wizard also checks for authentication settings that have been previously configured with hello wizard or are compatible with hello wizard.</span></span>  <span data-ttu-id="a3d79-115">Als alle instellingen aanwezig zijn, dit wordt beschouwd als een herhaalde aanvraag en Hallo wizard geopend Hallo instellingen weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a3d79-115">If all settings are present, it is considered a re-entrant case, and hello wizard opens display hello settings.</span></span>  <span data-ttu-id="a3d79-116">Als er slechts enkele van de instellingen Hallo aanwezig zijn, wordt het beschouwd als een foutaanvraag.</span><span class="sxs-lookup"><span data-stu-id="a3d79-116">If only some of hello settings are present, it is considered an error case.</span></span>

<span data-ttu-id="a3d79-117">In een MVC-project Hallo wizard controleert of een Hallo-instellingen, die het gevolg van eerdere gebruik van de wizard hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="a3d79-117">In an MVC project, hello wizard checks for any of hello following settings, which result from previous use of hello wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:AADInstance" value="" />
    <add key="ida:PostLogoutRedirectUri" value="" />

<span data-ttu-id="a3d79-118">Bovendien Hallo wizard controleert of een van de volgende instellingen in een Web API-project die het gevolg van eerdere gebruik van de wizard Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="a3d79-118">In addition, hello wizard checks for any of hello following settings in a Web API project, which result from previous use of hello wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:Audience" value="" />

### <a name="incompatible-authentication-code"></a><span data-ttu-id="a3d79-119">Niet-compatibele verificatiecode op te geven</span><span class="sxs-lookup"><span data-stu-id="a3d79-119">Incompatible Authentication Code</span></span>
<span data-ttu-id="a3d79-120">Ten slotte probeert Hallo wizard toodetect versies verificatiecode op te geven die zijn geconfigureerd met eerdere versies van Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a3d79-120">Finally, hello wizard attempts toodetect versions of authentication code that have been configured with previous versions of Visual Studio.</span></span> <span data-ttu-id="a3d79-121">Als u deze fout ontvangen, betekent dit dat het project bevat een incompatibel verificatietype.</span><span class="sxs-lookup"><span data-stu-id="a3d79-121">If you received this error, it means your project contains an incompatible authentication type.</span></span> <span data-ttu-id="a3d79-122">Hallo wizard detecteert Hallo volgende typen verificatie uit eerdere versies van Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="a3d79-122">hello wizard detects hello following types of authentication from previous versions of Visual Studio:</span></span>

* <span data-ttu-id="a3d79-123">Windows-verificatie</span><span class="sxs-lookup"><span data-stu-id="a3d79-123">Windows Authentication</span></span> 
* <span data-ttu-id="a3d79-124">Afzonderlijke gebruikersaccounts</span><span class="sxs-lookup"><span data-stu-id="a3d79-124">Individual User Accounts</span></span> 
* <span data-ttu-id="a3d79-125">Organisatieaccounts</span><span class="sxs-lookup"><span data-stu-id="a3d79-125">Organizational Accounts</span></span> 

<span data-ttu-id="a3d79-126">toodetect Windows-verificatie in een MVC-project Hallo wizard zoekt Hallo `authentication` element uit uw **web.config** bestand.</span><span class="sxs-lookup"><span data-stu-id="a3d79-126">toodetect Windows Authentication in an MVC project, hello wizard looks for hello `authentication` element from your **web.config** file.</span></span>

<pre>
    &lt;configuration&gt;
        &lt;system.web&gt;
            <span style="background-color: yellow">&lt;authentication mode="Windows" /&gt;</span>
        &lt;/system.web&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="a3d79-127">toodetect Windows-verificatie in een Web API-project Hallo wizard zoekt Hallo `IISExpressWindowsAuthentication` element van uw project **.csproj** bestand:</span><span class="sxs-lookup"><span data-stu-id="a3d79-127">toodetect Windows Authentication in a Web API project, hello wizard looks for hello `IISExpressWindowsAuthentication` element from your project's **.csproj** file:</span></span>

<pre>
    &lt;Project&gt;
        &lt;PropertyGroup&gt;
            <span style="background-color: yellow">&lt;IISExpressWindowsAuthentication&gt;enabled&lt;/IISExpressWindowsAuthentication&gt;</span>
        &lt;/PropertyGroup>
    &lt;/Project&gt;
</pre>

<span data-ttu-id="a3d79-128">verificatie van de afzonderlijke gebruikersaccounts toodetect, Hallo wizard zoekt Hallo pakket element uit uw **Packages.config** bestand.</span><span class="sxs-lookup"><span data-stu-id="a3d79-128">toodetect Individual User Accounts authentication, hello wizard looks for hello package element from your **Packages.config** file.</span></span>

<pre>
    &lt;packages&gt;
        <span style="background-color: yellow">&lt;package id="Microsoft.AspNet.Identity.EntityFramework" version="2.1.0" targetFramework="net45" /&gt;</span>
    &lt;/packages&gt;
</pre>

<span data-ttu-id="a3d79-129">toodetect een oude vorm van verificatie van de organisatie-Account, Hallo wizard zoekt Hallo-element van de volgende **web.config**:</span><span class="sxs-lookup"><span data-stu-id="a3d79-129">toodetect an old form of Organizational Account authentication, hello wizard looks for hello following element from **web.config**:</span></span>

<pre>
    &lt;configuration&gt;
        &lt;appSettings&gt;
            <span style="background-color: yellow">&lt;add key="ida:Realm" value="***" /&gt;</span>
        &lt;/appSettings&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="a3d79-130">verificatietype toochange hello, verwijder Hallo incompatibel verificatietype en Hallo wizard opnieuw uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="a3d79-130">toochange hello authentication type, remove hello incompatible authentication type and run hello wizard again.</span></span>

<span data-ttu-id="a3d79-131">Zie voor meer informatie [verificatie scenario's voor Azure AD](active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="a3d79-131">For more information, see [Authentication Scenarios for Azure AD](active-directory-authentication-scenarios.md).</span></span>

#<a name="next-steps"></a><span data-ttu-id="a3d79-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a3d79-132">Next steps</span></span>
- <span data-ttu-id="a3d79-133">[Authentication Scenarios for Azure AD](active-directory-authentication-scenarios.md) (Verificatiescenario's voor Azure AD)</span><span class="sxs-lookup"><span data-stu-id="a3d79-133">[Authentication Scenarios for Azure AD](active-directory-authentication-scenarios.md)</span></span>