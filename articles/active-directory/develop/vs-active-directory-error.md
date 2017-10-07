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
# <a name="diagnosing-errors-with-hello-azure-active-directory-connection-wizard"></a>Oplossen van problemen met Hallo Wizard van Azure Active Directory-verbinding
Hallo wizard gedetecteerd tijdens het detecteren van eerdere verificatiecode op te geven, een incompatibel verificatietype.   

## <a name="what-is-being-checked"></a>Wat wordt gecontroleerd?
**Opmerking:** toocorrectly vorige verificatiecode op te geven in een project detecteren, Hallo project moet worden gebouwd.  Als u deze fout is opgetreden en er geen een vorige verificatiecode op te geven in uw project, opnieuw en probeer het opnieuw.

### <a name="project-types"></a>Projecttypen
Hallo wizard controleert Hallo type project dat u ontwikkelt zodat deze Hallo rechts verificatielogica Hallo-project injecteren kan.  Als er domeincontroller die is afgeleid van `ApiController` in project Hallo Hallo-project wordt beschouwd als een WebAPI-project.  Als er alleen domeincontrollers die zijn afgeleid van `MVC.Controller` in project Hallo Hallo-project wordt beschouwd als een MVC-project.  Overige wordt niet ondersteund door de wizard Hallo.

### <a name="compatible-authentication-code"></a>Compatibel verificatiecode op te geven
Hallo wizard controleert ook of de verificatie-instellingen die eerder zijn geconfigureerd met de wizard Hallo of compatibel zijn met het Hallo-wizard.  Als alle instellingen aanwezig zijn, dit wordt beschouwd als een herhaalde aanvraag en Hallo wizard geopend Hallo instellingen weergegeven.  Als er slechts enkele van de instellingen Hallo aanwezig zijn, wordt het beschouwd als een foutaanvraag.

In een MVC-project Hallo wizard controleert of een Hallo-instellingen, die het gevolg van eerdere gebruik van de wizard hello te volgen:

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:AADInstance" value="" />
    <add key="ida:PostLogoutRedirectUri" value="" />

Bovendien Hallo wizard controleert of een van de volgende instellingen in een Web API-project die het gevolg van eerdere gebruik van de wizard Hallo Hallo:

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:Audience" value="" />

### <a name="incompatible-authentication-code"></a>Niet-compatibele verificatiecode op te geven
Ten slotte probeert Hallo wizard toodetect versies verificatiecode op te geven die zijn geconfigureerd met eerdere versies van Visual Studio. Als u deze fout ontvangen, betekent dit dat het project bevat een incompatibel verificatietype. Hallo wizard detecteert Hallo volgende typen verificatie uit eerdere versies van Visual Studio:

* Windows-verificatie 
* Afzonderlijke gebruikersaccounts 
* Organisatieaccounts 

toodetect Windows-verificatie in een MVC-project Hallo wizard zoekt Hallo `authentication` element uit uw **web.config** bestand.

<pre>
    &lt;configuration&gt;
        &lt;system.web&gt;
            <span style="background-color: yellow">&lt;authentication mode="Windows" /&gt;</span>
        &lt;/system.web&gt;
    &lt;/configuration&gt;
</pre>

toodetect Windows-verificatie in een Web API-project Hallo wizard zoekt Hallo `IISExpressWindowsAuthentication` element van uw project **.csproj** bestand:

<pre>
    &lt;Project&gt;
        &lt;PropertyGroup&gt;
            <span style="background-color: yellow">&lt;IISExpressWindowsAuthentication&gt;enabled&lt;/IISExpressWindowsAuthentication&gt;</span>
        &lt;/PropertyGroup>
    &lt;/Project&gt;
</pre>

verificatie van de afzonderlijke gebruikersaccounts toodetect, Hallo wizard zoekt Hallo pakket element uit uw **Packages.config** bestand.

<pre>
    &lt;packages&gt;
        <span style="background-color: yellow">&lt;package id="Microsoft.AspNet.Identity.EntityFramework" version="2.1.0" targetFramework="net45" /&gt;</span>
    &lt;/packages&gt;
</pre>

toodetect een oude vorm van verificatie van de organisatie-Account, Hallo wizard zoekt Hallo-element van de volgende **web.config**:

<pre>
    &lt;configuration&gt;
        &lt;appSettings&gt;
            <span style="background-color: yellow">&lt;add key="ida:Realm" value="***" /&gt;</span>
        &lt;/appSettings&gt;
    &lt;/configuration&gt;
</pre>

verificatietype toochange hello, verwijder Hallo incompatibel verificatietype en Hallo wizard opnieuw uitvoeren.

Zie voor meer informatie [verificatie scenario's voor Azure AD](active-directory-authentication-scenarios.md).

#<a name="next-steps"></a>Volgende stappen
- [Authentication Scenarios for Azure AD](active-directory-authentication-scenarios.md) (Verificatiescenario's voor Azure AD)