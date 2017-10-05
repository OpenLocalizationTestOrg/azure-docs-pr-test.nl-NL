---
title: Een Azure line-of-business-app maken met Azure Active Directory-verificatie | Microsoft Docs
description: Informatie over het maken van een ASP.NET MVC-line-of-business-app in Azure App Service die wordt geverifieerd met Azure Active Directory
services: app-service\web, active-directory
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: ad947bdb-4463-43ff-a5e3-91d9b2169b60
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 09/01/2016
ms.author: cephalin
ms.openlocfilehash: 6eadf0a521a32c5bc580908e4e4b7f4305e2bf7e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-line-of-business-azure-app-with-azure-active-directory-authentication"></a>Een Azure line-of-business-app maken met Azure Active Directory-verificatie
Dit artikel ziet u het maken van een line-of-business-app voor .NET in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) met behulp van de [verificatie / autorisatie](../app-service/app-service-authentication-overview.md) functie. Toont ook het gebruik van de [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) directorygegevens query in de toepassing.

De Azure Active Directory-tenant waarmee u mag een directory Azure alleen-lezen. Of het kan zijn [gesynchroniseerd met uw lokale Active Directory](../active-directory/active-directory-aadconnect.md) voor het maken van een ervaring voor eenmalige aanmelding voor werknemers die on-premises en extern zijn. In dit artikel gebruikt de standaarddirectory voor uw Azure-account.

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a>Wat u bouwt
Maakt u een eenvoudige regel-of-business maken, lezen, bijwerken, verwijderen (CRUD)-toepassing in App Service Web Apps dat nummers werkitems met de volgende functies:

* Verificatie van gebruikers met Azure Active Directory
* Query's Directory: gebruikers en groepen met behulp van [Azure Active Directory Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx)
* Gebruik de ASP.NET MVC *geen verificatie* sjabloon

Als u op rollen gebaseerde toegangsbeheer (RBAC) voor uw line-of-business-app in Azure nodig hebt, raadpleegt u [volgende stap](#next).

<a name="bkmk_need"></a>

## <a name="what-you-need"></a>Wat u nodig hebt
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

U moet het volgende om deze zelfstudie te voltooien:

* Een Azure Active Directory-tenant met gebruikers in verschillende groepen
* Machtigingen voor het maken van toepassingen op de Azure Active Directory-tenant
* Visual Studio 2013 Update 4 of hoger
* [Azure SDK 2.8.1 of hoger](https://azure.microsoft.com/downloads/)

<a name="bkmk_deploy"></a>

## <a name="create-and-deploy-a-web-app-to-azure"></a>Maken en implementeren van een web-app in Azure
1. Klik in Visual Studio op **bestand** > **nieuw** > **Project**.
2. Selecteer **ASP.NET-webtoepassing**, Geef uw project en klik op **OK**.
3. Selecteer de **MVC** sjabloon, wijzigt u vervolgens de authenticatie voor **geen verificatie**. Zorg ervoor dat **Host in de Cloud** is geselecteerd en klik op **OK**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/1-create-mvc-no-authentication.png)
4. In de **Create App Service** dialoogvenster, klikt u op **account toevoegen** (en vervolgens **account toevoegen** in de vervolgkeuzelijst) zich aanmelden bij uw Azure-account.
5. Zodra vastgelegd in uw web-app configureren. Een resourcegroep en een nieuwe App Service-abonnement maken door te klikken op de respectieve **nieuw** knop. Klik op **extra Azure-services verkennen** om door te gaan.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/2-create-app-service.png)
6. In de **Services** tabblad  **+**  toevoegen van een SQL-Database voor uw app. 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/3-add-sql-database.png)
7. In **SQL-Database configureren**, klikt u op **nieuw** voor het maken van een SQL Server-exemplaar.
8. In **SQL Server configureren**, configureren van uw SQL Server-exemplaar. Klik vervolgens op **OK**, **OK**, en **maken** Activeer het maken van de app in Azure.
9. In **Azure App Service-activiteit**, kunt u zien wanneer de app is gemaakt. Klik op  **publiceren &lt;* appname*> deze Web-App nu **, klik vervolgens op **publiceren**. 
   
    Zodra de Visual Studio is voltooid, wordt de app publiceren in de browser geopend. 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/4-published-shown-in-browser.png)

<a name="bkmk_auth"></a>

## <a name="configure-authentication-and-directory-access"></a>Verificatie- en -toegang configureren
1. Meld u aan bij [Azure Portal](https://portal.azure.com).
2. Klik in het menu links op **App Services** > **&lt;*appname*> ** > **verificatie / autorisatie**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/5-app-service-authentication.png)
3. Azure Active Directory-verificatie inschakelen door te klikken **op** > **Azure Active Directory** > **Express** > **OK**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/6-authentication-express.png)
4. Klik op **opslaan** in de opdrachtbalk.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/7-authentication-save.png)
   
    Als de verificatie-instellingen zijn opgeslagen, probeert u navigeren naar uw app opnieuw in de browser. De standaardinstellingen voor verificatie op de hele app worden afgedwongen. Als u al zijn niet aangemeld, wordt u omgeleid naar een aanmeldingsscherm. Nadat u bent aangemeld, ziet u uw app beveiligd door middel van HTTPS. Vervolgens moet u toegang tot Active directory-gegevens. 
5. Navigeer naar de [klassieke portal](https://manage.windowsazure.com).
6. Klik in het menu links op **Active Directory** > **standaarddirectory** > **toepassingen** > **&lt;*appname*> **.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/8-find-aad-application.png)
   
    Dit is de Azure Active Directory-toepassing die App Service voor u gemaakt waarmee de autorisatie / Authentication-functie.
7. Klik op **gebruikers** en **groepen** om ervoor te zorgen dat u sommige gebruikers en groepen in de map hebt. Als dit niet het geval is, is enkele testgebruikers en groepen maken.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/9-create-users-groups.png)
8. Klik op **configureren** om deze toepassing te configureren.
9. Schuif omlaag naar de **sleutels** gedeelte en een sleutel toevoegen door te selecteren van een duur. Klik vervolgens op **gedelegeerde machtigingen** en selecteer **mapgegevens lezen**. 
   Klik op **Opslaan**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/10-configure-aad-application.png)
10. Wanneer uw instellingen zijn opgeslagen, schuif terug tot de **sleutels** sectie en klik op de **kopie** knop om te kopiëren van de sleutel van de client. 
    
     ![](./media/web-sites-dotnet-lob-application-azure-ad/11-get-app-key.png)
    
    > [!IMPORTANT]
    > Als u deze pagina nu verlaat, kunt u niet de sleutel van deze client ooit opnieuw toegang tot.
    > 
    > 
11. Vervolgens moet u uw web-app configureren met deze sleutel. Meld u aan bij de [Azure Resource Explorer](https://resources.azure.com) met uw Azure-account.
12. Klik boven aan de pagina op **lezen/schrijven** wijzigingen aanbrengen in de Azure Resourceverkenner.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/12-resource-manager-writable.png)
13. De verificatie-instellingen voor uw app zich bevindt op abonnementen vinden >  **&lt;* subscriptionname*> ** > **resourceGroups** > **&lt;*resourcegroupname*> ** > **providers** > **Microsoft.Web** > **sites** > **&lt;*appname*> ** > **config** > **authsettings**.
14. Klik op **Bewerken**.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/13-edit-authsettings.png)
15. Stel in het deelvenster bewerken de `clientSecret` en `additionalLoginParams` eigenschappen als volgt.
    
        ...
        "clientSecret": "<client key from the Azure Active Directory application>",
        ...
        "additionalLoginParams": ["response_type=code id_token", "resource=https://graph.windows.net"],
        ...
16. Klik op **plaatsen** boven uw wijzigingen wilt indienen.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/14-edit-parameters.png)
17. Als u wilt testen als u het verificatietoken voor toegang tot Azure Active Directory Graph API hebt, navigeer nu naar  **https://&lt;*appname*>.azurewebsites.net/.auth/me** in uw browser. Als u alles correct geconfigureerd, ziet u de `access_token` eigenschap in het JSON-antwoord.
    
    De `~/.auth/me` URL-pad wordt beheerd door App Service-verificatie / autorisatie zodat u alle informatie die betrekking hebben op uw geverifieerde sessie. Zie voor meer informatie [verificatie en autorisatie in Azure App Service](../app-service/app-service-authentication-overview.md).
    
    > [!NOTE]
    > De `access_token` heeft een vervalperiode in. Echter App Service-verificatie / autorisatie biedt vernieuwingsfunctionaliteit token met `~/.auth/refresh`. Zie voor meer informatie over het gebruik ervan [App-Token servicearchief](https://cgillum.tech/2016/03/07/app-service-token-store/).
    > 
    > 

Vervolgens dient u iets nuttig met Active directory-gegevens.

<a name="bkmk_crud"></a>

## <a name="add-line-of-business-functionality-to-your-app"></a>Line-of-business-functionaliteit toevoegen aan uw app
U maakt nu een eenvoudige CRUD work items vastleggen.  

1. Maak een klassebestand WorkItem.cs aangeroepen in de map ~\Models en vervang `public class WorkItem {...}` met de volgende code:
   
     met behulp van System.ComponentModel.DataAnnotations;
   
     openbare klasse {werkitem
   
         [Key]
         public int ItemID { get; set; }
         public string AssignedToID { get; set; }
         public string AssignedToName { get; set; }
         public string Description { get; set; }
         public WorkItemStatus Status { get; set; }
     }
   
     openbare enum WorkItemStatus {
   
         Open,
         Investigating,
         Resolved,
         Closed
     }
2. Bouw het project voor het nieuwe model toegankelijk maken voor de logica steigers in Visual Studio.
3. Voeg een nieuw item in de gegenereerde `WorkItemsController` naar de map ~\Controllers (met de rechtermuisknop op **domeincontrollers**, wijs **toevoegen**, en selecteer **nieuw gegenereerde item**). 
4. Selecteer **MVC 5 Controller with views, using Entity Framework** en klik op **toevoegen**.
5. Selecteer het model dat u gemaakt en klik vervolgens op  **+**  en vervolgens **toevoegen** een gegevenscontext toevoegen en klik vervolgens op **toevoegen**.
   
   ![](./media/web-sites-dotnet-lob-application-azure-ad/16-add-scaffolded-controller.png)
6. Zoek in ~\Views\WorkItems\Create.cshtml (een automatisch gegenereerde artikel), de `Html.BeginForm` Help-methode en de volgende gemarkeerde wijzigingen aanbrengen:  
   
   <pre class="prettyprint">
   @model WebApplication1.Models.WorkItem
   
   @{
    ViewBag.Title = &quot;Create&quot;;
   }
   
   &lt;h2&gt;Create&lt;/h2&gt;
   
   @using (Html.BeginForm(<mark>&quot;Create&quot;, &quot;WorkItems&quot;, FormMethod.Post, new { id = &quot;main-form&quot; }</mark>)) 
   {
    @Html.AntiForgeryToken()
   
    &lt;div class=&quot;form-horizontal&quot;&gt;
        &lt;h4&gt;WorkItem&lt;/h4&gt;
        &lt;hr /&gt;
        @Html.ValidationSummary(true, &quot;&quot;, new { @class = &quot;text-danger&quot; })
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToID, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToID, new { htmlAttributes = new { @class = &quot;form-control&quot;<mark>, @type = &quot;hidden&quot;</mark> } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToID, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToName, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToName, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToName, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Description, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.Description, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.Description, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EnumDropDownListFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;form-control&quot; })
                @Html.ValidationMessageFor(model =&gt; model.Status, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            &lt;div class=&quot;col-md-offset-2 col-md-10&quot;&gt;
                &lt;input type=&quot;submit&quot; value=&quot;Create&quot; class=&quot;btn btn-default&quot;<mark> id=&quot;submit-button&quot;</mark> /&gt;
            &lt;/div&gt;
        &lt;/div&gt;
    &lt;/div&gt;
   }
   
   &lt;div&gt;
    @Html.ActionLink(&quot;Back to List&quot;, &quot;Index&quot;)
   &lt;/div&gt;
   
   @section Scripts {
    @Scripts.Render(&quot;~/bundles/jqueryval&quot;)
    <mark>&lt;script&gt;
        // People/Group Picker Code
        var maxResultsPerPage = 14;
        var input = document.getElementById(&quot;AssignedToName&quot;);
   
        // Access token from request header, and tenantID from claims identity
        var token = &quot;@Request.Headers[&quot;X-MS-TOKEN-AAD-ACCESS-TOKEN&quot;]&quot;;
        var tenant =&quot;@(System.Security.Claims.ClaimsPrincipal.Current.Claims
                        .Where(c => c.Type == &quot;http://schemas.microsoft.com/identity/claims/tenantid&quot;)
                        .Select(c => c.Value).SingleOrDefault())&quot;;
   
        var picker = new AadPicker(maxResultsPerPage, input, token, tenant);
   
        // Submit the selected user/group to be asssigned.
        $(&quot;#submit-button&quot;).click({ picker: picker }, function () {
            if (!picker.Selected())
                return;
            $(&quot;#main-form&quot;).get()[0].elements[&quot;AssignedToID&quot;].value = picker.Selected().objectId;
        });
    &lt;/script&gt;</mark>
   }
   </pre>
   
   Houd er rekening mee dat `token` en `tenant` worden gebruikt door de `AadPicker` object Azure Active Directory Graph API-aanroepen. U voegt `AadPicker` later.     
   
   > [!NOTE]
   > U krijgt net zo goed `token` en `tenant` vanaf de client met `~/.auth/me`, maar dat zou de aanroep van een extra server. Bijvoorbeeld:
   > 
   > $.ajax ({dataType: 'json', url: '/.auth/me', succes: functie (gegevens) {var token gegevens [0] = .access_token; var tenant = gegevens [0] .user_claims .find (c = > c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val;}});
   > 
   > 
7. Met dezelfde wijzigingen aanbrengen ~ \Views\WorkItems\Edit.cshtml.
8. De `AadPicker` -object is gedefinieerd in een script dat u wilt toevoegen aan uw project. Met de rechtermuisknop op de map ~\Scripts, wijst u **toevoegen**, en klik op **JavaScript-bestand**. Type `AadPickerLibrary` voor de bestandsnaam en klik op **OK**.
9. Kopieer de inhoud van [hier](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) in ~ \Scripts\AadPickerLibrary.js.
   
   In het script wordt de `AadPicker` object aanroepen [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) om te zoeken naar gebruikers en groepen die overeenkomen met de invoer.  
10. ~\Scripts\AadPickerLibrary.js gebruikt ook de [jQuery gebruikersinterface automatisch aanvullen widget](https://jqueryui.com/autocomplete/). U moet dus jQuery UI toevoegen aan uw project. Met de rechtermuisknop op het project in en klik op **NuGet-pakketten beheren**.
11. In de NuGet Package Manager, klikt u op Bladeren, type **jquery-ui** in de zoekbalk en op **jQuery.UI.Combined**.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/17-add-jquery-ui-nuget.png)
12. Klik in het rechterdeelvenster **installeren**, klikt u vervolgens op **OK** om door te gaan.
13. Open ~\App_Start\BundleConfig.cs en de volgende gemarkeerde wijzigingen aanbrengen:  
    
    <pre class="prettyprint">
    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle(&quot;~/bundles/jquery&quot;).Include(
                    &quot;~/Scripts/jquery-{version}.js&quot;<mark>,
                    &quot;~/Scripts/jquery-ui-{version}.js&quot;,
                    &quot;~/Scripts/AadPickerLibrary.js&quot;</mark>));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/jqueryval&quot;).Include(
                    &quot;~/Scripts/jquery.validate*&quot;));
    
        // Use the development version of Modernizr to develop with and learn from. Then, when you&#39;re
        // ready for production, use the build tool at http://modernizr.com to pick only the tests you need.
        bundles.Add(new ScriptBundle(&quot;~/bundles/modernizr&quot;).Include(
                    &quot;~/Scripts/modernizr-*&quot;));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/bootstrap&quot;).Include(
                    &quot;~/Scripts/bootstrap.js&quot;,
                    &quot;~/Scripts/respond.js&quot;));
    
        bundles.Add(new StyleBundle(&quot;~/Content/css&quot;).Include(
                    &quot;~/Content/bootstrap.css&quot;,
                    &quot;~/Content/site.css&quot;<mark>,
                    &quot;~/Content/themes/base/jquery-ui.css&quot;</mark>));
    }
    </pre>
    
    Er zijn meer zodat manieren voor het beheren van JavaScript en CSS-bestanden in uw app. Echter voor eenvoud gaat net u op de pakketten die worden geladen met elke weergave worden gemaakt.
14. Ten slotte in ~ \Global.asax, voeg de volgende regel code in de `Application_Start()` methode. `Ctrl`+`.`op elke naming omzettingsfout om dit te herstellen.
    
        AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.NameIdentifier;
    
    > [!NOTE]
    > U moet deze coderegel omdat de standaard MVC-sjabloon gebruikt <code>[ValidateAntiForgeryToken]</code> decoration op enkele van de acties. Als gevolg van het gedrag beschreven door [Brock Allen](https://twitter.com/BrockLAllen) op [MVC 4, AntiForgeryToken en Claims](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) uw HTTP POST ter voorkoming validatie van tokens kan mislukken omdat:
    > 
    > * Azure Active Directory verzendt de http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider die wordt standaard door de anti-vervalsingstoken vereist.
    > * Als Azure Active Directory directory gesynchroniseerd met AD FS, verzendt de vertrouwensrelatie van de AD FS standaard de claim http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider, maar u kunt AD FS voor het verzenden van deze claim handmatig configureren.
    > 
    > `ClaimTypes.NameIdentifies`Hiermee geeft u de claim `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, die Azure Active Directory levert.  
    > 
    > 
15. Publiceer nu uw wijzigingen. Met de rechtermuisknop op uw project en klik op **publiceren**.
16. Klik op **instellingen**, zorg ervoor dat er een verbindingsreeks voor de SQL-Database, selecteert u **Database bijwerken** om u aan te maken van de wijzigingen in het schema voor het model, klik op **publiceren**.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/18-publish-crud-changes.png)
17. Navigeer in de browser naar https://&lt;*appname*>.azurewebsites.net/workitems en klikt u op **nieuw**.
18. Klik in de **AssignedToName** vak. U ziet nu gebruikers en groepen van uw Azure Active Directory-tenant in een vervolgkeuzelijst. Typ om te filteren of gebruik de `Up` of `Down` sleutel of schakelt u de gebruiker of groep. 
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/19-use-aadpicker.png)
19. Klik op **maken** de wijzigingen wilt opslaan. Klik vervolgens op **bewerken** op het gemaakte werkitem hetzelfde gedrag in acht nemen.

Gefeliciteerd, uitvoert u nu een line-of-business-app in Azure met toegang tot directory! Er is veel meer dat kunt u doen met de Graph API. Zie [Azure AD Graph API-referentiemateriaal](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).

<a name="next"></a>

## <a name="next-step"></a>Volgende stap
Als u op rollen gebaseerde toegangsbeheer (RBAC) voor uw line-of-business-app in azure nodig hebt, raadpleegt u [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) voor een voorbeeld van het team van Azure Active Directory. Hier ziet u het inschakelen van functies voor uw Azure Active Directory-toepassing en vervolgens het autoriseren van gebruikers met de `[Authorize]` decoration.

Als uw line-of-business-app toegang tot on-premises gegevens moet, Zie [toegang tot on-premises resources met behulp van hybride verbindingen in Azure App Service](web-sites-hybrid-connection-get-started.md).

<a name="bkmk_resources"></a>

## <a name="further-resources"></a>Meer bronnen
* [Verificatie en autorisatie in Azure App Service](../app-service/app-service-authentication-overview.md)
* [Verificatie met de on-premises Active Directory in uw app in Azure](web-sites-authentication-authorization.md)
* [Een line-of-business-app in Azure maken met AD FS-authenticatie](web-sites-dotnet-lob-application-adfs.md)
* [App Service-verificatie en Azure AD Graph API](https://cgillum.tech/2016/03/25/app-service-auth-aad-graph-api/)
* [Microsoft Azure Active Directory-voorbeelden en documentatie](https://github.com/AzureADSamples)
* [Azure Active Directory ondersteund Token en claimtypen](http://msdn.microsoft.com/library/azure/dn195587.aspx)
