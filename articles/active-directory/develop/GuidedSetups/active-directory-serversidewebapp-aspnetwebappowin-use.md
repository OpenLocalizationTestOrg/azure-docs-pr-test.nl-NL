---
title: aaaAzure AD v2 ASP.NET Web Server aan de slag - gebruik | Microsoft Docs
description: Implementeren van Microsoft-aanmeldingspagina op een ASP.NET-oplossing met een traditioneel browser gebaseerde webtoepassing met behulp van standaard OpenID Connect
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 03afce6fa6598215e8c4af841c00762c143a0cd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="add-a-controller-toohandle-sign-in-and-sign-out-requests"></a>Toevoegen van een domeincontroller toohandle aanmelden en afmeldingsaanvragen te verzenden

Deze stap wordt weergegeven hoe een nieuwe domeincontroller tooexpose toocreate aanmelden en afmeldingsmethoden toe.

1.  Klik met de rechtermuisknop op Hallo `Controllers` map en selecteer`Add` > `Controller`
2.  Selecteer `MVC (.NET version) Controller – Empty`.
3.  Klik op *toevoegen*
4.  Naam `HomeController` en klik op *toevoegen*
5.  Voeg *OWIN* verwijst naar toohello klasse:

```csharp
using Microsoft.Owin.Security;
using Microsoft.Owin.Security.Cookies;
using Microsoft.Owin.Security.OpenIdConnect;
```
<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
Hallo twee methoden hieronder toohandle aanmelden en afmelden tooyour controller toevoegen door een verificatievraag via code initiëren:
</li>
</ol>

```csharp
/// <summary>
/// Send an OpenID Connect sign-in request.
/// Alternatively, you can just decorate hello SignIn method with hello [Authorize] attribute
/// </summary>
public void SignIn()
{
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge(
            new AuthenticationProperties{ RedirectUri = "/" },
            OpenIdConnectAuthenticationDefaults.AuthenticationType);
    }
}

/// <summary>
/// Send an OpenID Connect sign-out request.
/// </summary>
public void SignOut()
{
    HttpContext.GetOwinContext().Authentication.SignOut(
            OpenIdConnectAuthenticationDefaults.AuthenticationType,
            CookieAuthenticationDefaults.AuthenticationType);
}
```

## <a name="create-hello-apps-home-page-toosign-in-users-via-a-sign-in-button"></a>Hallo-app startpagina toosign in gebruikers via een knop maken

Maak een nieuwe weergave tooadd Hallo aanmelden knop in Visual Studio en gebruikersgegevens na verificatie weergeven:

1.  Klik met de rechtermuisknop op Hallo `Views\Home` map en selecteer`Add View`
2.  Noem deze `Index`.
3.  Hallo HTML-code, waaronder het Hallo-knop aanmelden, toohello bestand volgende toevoegen:

```html
<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>Sign-In with Microsoft Guide</title>
</head>
<body>
@if (!Request.IsAuthenticated)
{
    <!-- If hello user is not authenticated, display hello sign-in button -->
    <a href="@Url.Action("SignIn", "Home")" style="text-decoration: none;">
        <svg xmlns="http://www.w3.org/2000/svg" xml:space="preserve" width="300px" height="50px" viewBox="0 0 3278 522" class="SignInButton">
        <style type="text/css">.fil0:hover {fill: #4B4B4B;} .fnt0 {font-size: 260px;font-family: 'Segoe UI Semibold', 'Segoe UI'; text-decoration: none;}</style>
        <rect class="fil0" x="2" y="2" width="3174" height="517" fill="black" />
        <rect x="150" y="129" width="122" height="122" fill="#F35325" />
        <rect x="284" y="129" width="122" height="122" fill="#81BC06" />
        <rect x="150" y="263" width="122" height="122" fill="#05A6F0" />
        <rect x="284" y="263" width="122" height="122" fill="#FFBA08" />
        <text x="470" y="357" fill="white" class="fnt0">Sign in with Microsoft</text>
        </svg>
    </a>
}
else
{
    <span><br/>Hello @System.Security.Claims.ClaimsPrincipal.Current.FindFirst("name").Value;</span>
    <br /><br />
    @Html.ActionLink("See Your Claims", "Index", "Claims")
    <br /><br />
    @Html.ActionLink("Sign out", "SignOut", "Home")
}
@if (!string.IsNullOrWhiteSpace(Request.QueryString["errormessage"]))
{
    <div style="background-color:red;color:white;font-weight: bold;">Error: @Request.QueryString["errormessage"]</div>
}
</body>
</html>
```
<!--start-collapse-->
### <a name="more-information"></a>Meer informatie
> Deze pagina wordt de knop aanmelden in SVG-indeling met een zwarte achtergrond toegevoegd:<br/>![Aanmelden met Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-use/aspnetsigninbuttonsample.png)<br/> Ga voor meer aanmelden knoppen toohello [deze pagina](https://docs.microsoft.com/azure/active-directory/develop/active-directory-branding-guidelines "richtlijnen huisstijl").
<!--end-collapse-->

## <a name="add-a-controller-toodisplay-users-claims"></a>Claims van een domeincontroller toodisplay gebruiker toe te voegen
Deze domeincontroller wordt gedemonstreerd Hallo maakt gebruik van Hallo `[Authorize]` kenmerk tooprotect een domeincontroller. Dit kenmerk beperkt toegang toohello controller door alleen geverifieerde gebruikers. Hallo code hieronder maakt gebruik van Hallo kenmerk toodisplay gebruikersclaims die zijn opgehaald als onderdeel van Hallo aanmelden.

1.  Klik met de rechtermuisknop op Hallo `Controllers` map:`Add` > `Controller`
2.  Selecteer `MVC {version} Controller – Empty`.
3.  Klik op *toevoegen*
4.  Geef deze de naam`ClaimsController`
5.  Vervang Hallo-code van uw controllerklasse met Hallo-code hieronder - Hiermee voegt u Hallo `[Authorize]` toohello kenmerkklasse:

```csharp
[Authorize]
public class ClaimsController : Controller
{
    /// <summary>
    /// Add user's claims tooviewbag
    /// </summary>
    /// <returns></returns>
    public ActionResult Index()
    {
        var claimsPrincipalCurrent = System.Security.Claims.ClaimsPrincipal.Current;
        //You get hello user’s first and last name below:
        ViewBag.Name = claimsPrincipalCurrent.FindFirst("name").Value;

        // hello 'preferred_username' claim can be used for showing hello username
        ViewBag.Username = claimsPrincipalCurrent.FindFirst("preferred_username").Value;

        // hello subject claim can be used toouniquely identify hello user across hello web
        ViewBag.Subject = claimsPrincipalCurrent.FindFirst(System.Security.Claims.ClaimTypes.NameIdentifier).Value;

        // TenantId is hello unique Tenant Id - which represents an organization in Azure AD
        ViewBag.TenantId = claimsPrincipalCurrent.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;

        return View();
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a>Meer informatie
> Vanwege het gebruik van Hallo Hallo `[Authorize]` kenmerk, alle methoden van deze domeincontroller kan alleen worden uitgevoerd als het Hallo-gebruiker is geverifieerd. Hallo-gebruiker is niet geverifieerd en probeert tooaccess Hallo controller, wordt OWIN een verificatievraag starten als Hallo gebruiker tooauthenticate afdwingen. Hallo bovenstaande lijkt op Hallo code claims verzameling Hallo `ClaimsPrincipal.Current` -exemplaar voor een specifieke gebruikerskenmerken in Hallo gebruikerstoken. Deze kenmerken zijn volledige naam van de gebruiker Hallo en username, evenals Hallo globale id onderwerp. Het bevat ook Hallo *Tenant-ID*, die Hallo-ID voor de organisatie van de gebruiker Hallo vertegenwoordigt. 
<!--end-collapse-->

## <a name="create-a-view-toodisplay-hello-users-claims"></a>Een weergave maken toodisplay Hallo claims van de gebruiker

Maak een nieuwe weergave toodisplay Hallo claims van de gebruiker in een webpagina in Visual Studio:

1.  Klik met de rechtermuisknop op Hallo `Views\Claims` map en:`Add View`
2.  Noem deze `Index`.
3.  Hallo HTML-bestand voor toohello volgende toevoegen:

```html
<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>Sign-In with Microsoft Sample</title>
    <link href="@Url.Content("~/Content/bootstrap.min.css")" rel="stylesheet" type="text/css" />
</head>
<body style="padding:50px">
    <h3>Main Claims:</h3>
    <table class="table table-striped table-bordered table-hover">
        <tr><td>Name</td><td>@ViewBag.Name</td></tr>
        <tr><td>Username</td><td>@ViewBag.Username</td></tr>
        <tr><td>Subject</td><td>@ViewBag.Subject</td></tr>
        <tr><td>TenantId</td><td>@ViewBag.TenantId</td></tr>
    </table>
    <br />
    <h3>All Claims:</h3>
    <table class="table table-striped table-bordered table-hover table-condensed">
    @foreach (var claim in System.Security.Claims.ClaimsPrincipal.Current.Claims)
    {
        <tr><td>@claim.Type</td><td>@claim.Value</td></tr>
    }
</table>
    <br />
    <br />
    @Html.ActionLink("Sign out", "SignOut", "Home", null, new { @class = "btn btn-primary" })
</body>
</html>
```
