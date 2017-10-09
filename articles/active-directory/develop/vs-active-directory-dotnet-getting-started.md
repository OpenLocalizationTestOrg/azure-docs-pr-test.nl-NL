---
title: aaaGet gestart met Azure AD in Visual Studio MVC projecten | Microsoft Docs
description: Hoe tooget gestart met behulp van Azure Active Directory in MVC projecten nadat u verbinding maken van een Azure AD met Visual Studio tooor hebt verbonden services
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1c8b6a58-5144-4965-a905-625b9ee7b22b
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 807824dd6e4e57e443f8a7322cf2e5326384316d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-active-directory-and-visual-studio-connected-services-mvc-projects"></a>Aan de slag met Azure Active Directory en Visual Studio verbonden services (MVC-projecten)
> [!div class="op_single_selector"]
> * [Aan de slag](vs-active-directory-dotnet-getting-started.md)
> * [Wat is er gebeurd](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="requiring-authentication-tooaccess-controllers"></a>Verificatie tooaccess domeincontrollers vereisen
Alle domeincontrollers in uw project zijn adorned Hello **autoriseren** kenmerk. Dit kenmerk moet Hallo gebruiker toobe geverifieerd voordat toegang tot deze controllers. Dit kenmerk tooallow Hallo controller toobe anoniem, gebruikt verwijderen uit Hallo-controller. Als u tooset Hallo machtigingen op een meer gedetailleerd niveau wilt, kunt u Hallo kenmerk tooeach methode waarvoor de autorisatie in plaats van het toepassen van toohello controllerklasse toepassen.

## <a name="adding-signin--signout-controls"></a>Toevoegen van aanmelding / SignOut besturingselementen
tooadd hello aanmelding/SignOut besturingselementen tooyour weergeven, kunt u Hallo **_LoginPartial.cshtml** gedeeltelijke weergave tooadd Hallo functionaliteit tooone van uw weergaven. Hier volgt een voorbeeld van Hallo functionaliteit toegevoegd toohello standaard **_Layout.cshtml** weergeven. (Houd er rekening mee Hallo laatste element in Hallo div met de klasse navigatiebalk samenvouwen):

<pre>
    &lt;!DOCTYPE html&gt; 
     &lt;html&gt; 
     &lt;head&gt; 
         &lt;meta charset="utf-8" /&gt; 
        &lt;meta name="viewport" content="width=device-width, initial-scale=1.0"&gt; 
        &lt;title&gt;@ViewBag.Title - My ASP.NET Application&lt;/title&gt; 
        @Styles.Render("~/Content/css") 
        @Scripts.Render("~/bundles/modernizr") 
    &lt;/head&gt; 
    &lt;body&gt; 
        &lt;div class="navbar navbar-inverse navbar-fixed-top"&gt; 
            &lt;div class="container"&gt; 
                &lt;div class="navbar-header"&gt; 
                    &lt;button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse"&gt; 
                        &lt;span class="icon-bar"&gt;&lt;/span&gt; 
                        &lt;span class="icon-bar"&gt;&lt;/span&gt; 
                        &lt;span class="icon-bar"&gt;&lt;/span&gt; 
                    &lt;/button&gt; 
                    @Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" }) 
                &lt;/div&gt; 
                &lt;div class="navbar-collapse collapse"&gt; 
                    &lt;ul class="nav navbar-nav"&gt; 
                        &lt;li&gt;@Html.ActionLink("Home", "Index", "Home")&lt;/li&gt; 
                        &lt;li&gt;@Html.ActionLink("About", "About", "Home")&lt;/li&gt; 
                        &lt;li&gt;@Html.ActionLink("Contact", "Contact", "Home")&lt;/li&gt; 
                    &lt;/ul&gt; 
                    <span style="background-color:yellow">@Html.Partial("_LoginPartial")</span> 
                &lt;/div&gt; 
            &lt;/div&gt; 
        &lt;/div&gt; 
        &lt;div class="container body-content"&gt; 
            @RenderBody() 
            &lt;hr /&gt; 
            &lt;footer&gt; 
                &lt;p&gt;&amp;copy; @DateTime.Now.Year - My ASP.NET Application&lt;/p&gt; 
            &lt;/footer&gt; 
        &lt;/div&gt; 
        @Scripts.Render("~/bundles/jquery") 
        @Scripts.Render("~/bundles/bootstrap") 
        @RenderSection("scripts", required: false) 
    &lt;/body&gt; 
    &lt;/html&gt;
</pre>

## <a name="next-steps"></a>Volgende stappen
- [Meer informatie over Azure Active Directory](https://azure.microsoft.com/services/active-directory/) 

