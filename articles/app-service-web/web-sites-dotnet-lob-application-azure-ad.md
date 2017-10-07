---
title: een Azure line-of-business-app met Azure Active Directory-verificatie aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een ASP.NET MVC line-of-business-app in Azure App Service die wordt geverifieerd met Azure Active Directory
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
ms.openlocfilehash: 3bcafad78ac0151889b3e336784cc561009f244f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-azure-active-directory-authentication"></a>Een Azure line-of-business-app maken met Azure Active Directory-verificatie
Dit artikel ziet u hoe toocreate een .NET line-of-business-app in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) met Hallo [verificatie / autorisatie](../app-service/app-service-authentication-overview.md) functie. U ziet ook hoe toouse hello [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) tooquery directory-gegevens in de toepassing hello.

Hello Azure Active Directory-tenant waarmee u mag een directory Azure alleen-lezen. Of het kan zijn [gesynchroniseerd met uw lokale Active Directory](../active-directory/active-directory-aadconnect.md) toocreate een ervaring voor eenmalige aanmelding voor werknemers die on-premises en externe. In dit artikel gebruikt Hallo standaarddirectory voor uw Azure-account.

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a>Wat u bouwt
Maakt u een eenvoudige regel-of-business maken, lezen, bijwerken, verwijderen (CRUD)-toepassing in App Service Web Apps dat nummers items werken met Hallo volgende kenmerken:

* Verificatie van gebruikers met Azure Active Directory
* Query's Directory: gebruikers en groepen met behulp van [Azure Active Directory Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx)
* Gebruik ASP.NET MVC Hallo *geen verificatie* sjabloon

Als u op rollen gebaseerde toegangsbeheer (RBAC) voor uw line-of-business-app in Azure nodig hebt, raadpleegt u [volgende stap](#next).

<a name="bkmk_need"></a>

## <a name="what-you-need"></a>Wat u nodig hebt
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

U moet volgen toocomplete Hallo in deze zelfstudie:

* Een Azure Active Directory-tenant met gebruikers in verschillende groepen
* Machtigingen toocreate toepassingen op Hallo Azure Active Directory-tenant
* Visual Studio 2013 Update 4 of hoger
* [Azure SDK 2.8.1 of hoger](https://azure.microsoft.com/downloads/)

<a name="bkmk_deploy"></a>

## <a name="create-and-deploy-a-web-app-tooazure"></a>Maken en implementeren van een web-app tooAzure
1. Klik in Visual Studio op **bestand** > **nieuw** > **Project**.
2. Selecteer **ASP.NET-webtoepassing**, Geef uw project en klik op **OK**.
3. Selecteer Hallo **MVC** sjabloon, wijzigt u vervolgens de Hallo verificatie te**geen verificatie**. Zorg ervoor dat **Host in Cloud Hallo** is geselecteerd en klik op **OK**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/1-create-mvc-no-authentication.png)
4. In Hallo **Create App Service** dialoogvenster, klikt u op **account toevoegen** (en vervolgens **account toevoegen** Hallo vervolgkeuzelijst) toolog in tooyour Azure-account.
5. Zodra vastgelegd in uw web-app configureren. Een resourcegroep en een nieuwe App Service-abonnement maken door te klikken op Hallo respectieve **nieuw** knop. Klik op **extra Azure-services verkennen** toocontinue.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/2-create-app-service.png)
6. In Hallo **Services** tabblad  **+**  tooadd een SQL-Database voor uw app. 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/3-add-sql-database.png)
7. In **SQL-Database configureren**, klikt u op **nieuw** toocreate een exemplaar van SQL Server.
8. In **SQL Server configureren**, configureren van uw SQL Server-exemplaar. Klik vervolgens op **OK**, **OK**, en **maken** tookick uit Hallo app gemaakt in Azure.
9. In **Azure App Service-activiteit**, kunt u zien wanneer Hallo app is gemaakt. Klik op  **publiceren &lt;* appname*> toothis Web-App nu **, klikt u vervolgens op **publiceren**. 
   
    Als Visual Studio is voltooid, Open het Hallo app publiceren in Hallo browser. 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/4-published-shown-in-browser.png)

<a name="bkmk_auth"></a>

## <a name="configure-authentication-and-directory-access"></a>Verificatie- en -toegang configureren
1. Meld u bij toohello [Azure-portal](https://portal.azure.com).
2. In het linkermenu hello, klikt u op **App Services** > **&lt;*appname*> ** > **verificatie / autorisatie**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/5-app-service-authentication.png)
3. Azure Active Directory-verificatie inschakelen door te klikken **op** > **Azure Active Directory** > **Express** > **OK**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/6-authentication-express.png)
4. Klik op **opslaan** in de opdrachtbalk Hallo.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/7-authentication-save.png)
   
    Zodra Hallo verificatie-instellingen zijn opgeslagen, kunt u proberen opnieuw in de browser Hallo tooyour app navigeren. De standaardinstellingen voor afdwingen verificatie op de hele app Hallo. Als u al zijn niet aangemeld, bent u omgeleide tooa aanmeldingsscherm. Nadat u bent aangemeld, ziet u uw app beveiligd door middel van HTTPS. Vervolgens moet u tooenable access toodirectory-gegevens. 
5. Navigeer toohello [klassieke portal](https://manage.windowsazure.com).
6. In het linkermenu hello, klikt u op **Active Directory** > **standaarddirectory** > **toepassingen**  >   **&lt;* appname*> **.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/8-find-aad-application.png)
   
    Dit is hello Azure Active Directory-toepassing die App Service voor u tooenable Hallo autorisatie gemaakt / Authentication-functie.
7. Klik op **gebruikers** en **groepen** toomake ervoor dat u sommige gebruikers en groepen in Hallo map hebt. Als dit niet het geval is, is enkele testgebruikers en groepen maken.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/9-create-users-groups.png)
8. Klik op **configureren** tooconfigure deze toepassing.
9. Schuif omlaag toohello **sleutels** gedeelte en een sleutel toevoegen door te selecteren van een duur. Klik vervolgens op **gedelegeerde machtigingen** en selecteer **mapgegevens lezen**. 
   Klik op **Opslaan**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/10-configure-aad-application.png)
10. Wanneer uw instellingen zijn opgeslagen, schuif back-up toohello **sleutels** sectie en klikt u op Hallo **kopie** sleutel van de knop toocopy Hallo-client. 
    
     ![](./media/web-sites-dotnet-lob-application-azure-ad/11-get-app-key.png)
    
    > [!IMPORTANT]
    > Als u deze pagina nu verlaat, u niet kunt tooaccess deze client sleutel ooit opnieuw.
    > 
    > 
11. Vervolgens moet u tooconfigure uw web-app met deze sleutel. Meld u bij toohello [Azure Resource Explorer](https://resources.azure.com) met uw Azure-account.
12. Bovenaan Hallo Hallo pagina, klikt u op **lezen/schrijven** toomake wijzigingen in hello Azure Resource Explorer.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/12-resource-manager-writable.png)
13. Hallo zoeken verificatie-instellingen voor uw app zich bevindt op abonnementen >  **&lt;* subscriptionname*> ** > **resourceGroups**  >   **&lt;* resourcegroupname*> ** > **providers** > **Microsoft.Web**  >  **sites** > **&lt;*appname*> ** > **config**  >  **authsettings**.
14. Klik op **Bewerken**.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/13-edit-authsettings.png)
15. In Hallo deelvenster bewerken, stelt u Hallo `clientSecret` en `additionalLoginParams` eigenschappen als volgt.
    
        ...
        "clientSecret": "<client key from hello Azure Active Directory application>",
        ...
        "additionalLoginParams": ["response_type=code id_token", "resource=https://graph.windows.net"],
        ...
16. Klik op **plaatsen** op Hallo bovenste toosubmit worden uw wijzigingen.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/14-edit-parameters.png)
17. Nu tootest hebt u Hallo autorisatie token tooaccess hello Azure Active Directory Graph API, gaat u naar  **https://&lt;*appname*>.azurewebsites.net/.auth/me** in uw Browser. Als u alles correct geconfigureerd, ziet u Hallo `access_token` eigenschap in Hallo JSON-antwoord.
    
    Hallo `~/.auth/me` URL-pad wordt beheerd door App Service-verificatie / autorisatie toogive u alle Hallo informatie over de tooyour geverifieerde sessie. Zie voor meer informatie [verificatie en autorisatie in Azure App Service](../app-service/app-service-authentication-overview.md).
    
    > [!NOTE]
    > Hallo `access_token` heeft een vervalperiode in. Echter App Service-verificatie / autorisatie biedt vernieuwingsfunctionaliteit token met `~/.auth/refresh`. Voor meer informatie over het toouse, Zie [App-Token servicearchief](https://cgillum.tech/2016/03/07/app-service-token-store/).
    > 
    > 

Vervolgens dient u iets nuttig met Active directory-gegevens.

<a name="bkmk_crud"></a>

## <a name="add-line-of-business-functionality-tooyour-app"></a>Line-of-business-functionaliteit tooyour app toevoegen
U maakt nu een eenvoudige CRUD work items vastleggen.  

1. Hallo ~\Models map, maakt u een klassebestand WorkItem.cs aangeroepen en vervang `public class WorkItem {...}` Hello code te volgen:
   
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
2. De juiste Hallo project toomake uw nieuwe model toegankelijk toohello steigers logica in Visual Studio.
3. Toevoegen van een nieuw item in de gegenereerde `WorkItemsController` toohello ~\Controllers map (met de rechtermuisknop op **domeincontrollers**, wijst u te**toevoegen**, en selecteer **nieuw gegenereerde item**). 
4. Selecteer **MVC 5 Controller with views, using Entity Framework** en klik op **toevoegen**.
5. Selecteer Hallo model dat u hebt gemaakt, klikt u vervolgens op  **+**  en vervolgens **toevoegen** tooadd een gegevenscontext en klik vervolgens op **toevoegen**.
   
   ![](./media/web-sites-dotnet-lob-application-azure-ad/16-add-scaffolded-controller.png)
6. Zoek in ~\Views\WorkItems\Create.cshtml (een automatisch gegenereerde artikel), Hallo `Html.BeginForm` Help-methode en Hallo volgende gemarkeerde wijzigingen aanbrengen:  
   
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
    @Html.ActionLink(&quot;Back tooList&quot;, &quot;Index&quot;)
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
   
        // Submit hello selected user/group toobe asssigned.
        $(&quot;#submit-button&quot;).click({ picker: picker }, function () {
            if (!picker.Selected())
                return;
            $(&quot;#main-form&quot;).get()[0].elements[&quot;AssignedToID&quot;].value = picker.Selected().objectId;
        });
    &lt;/script&gt;</mark>
   }
   </pre>
   
   Houd er rekening mee dat `token` en `tenant` worden gebruikt door Hallo `AadPicker` object toomake Azure Active Directory Graph API-aanroepen. U voegt `AadPicker` later.     
   
   > [!NOTE]
   > Net zo goed kunt u krijgen `token` en `tenant` vanaf clientzijde Hallo met `~/.auth/me`, maar dat de aanroep van een extra server zou zijn. Bijvoorbeeld:
   > 
   > $.ajax ({dataType: 'json', url: '/.auth/me', succes: functie (gegevens) {var token gegevens [0] = .access_token; var tenant = gegevens [0] .user_claims .find (c = > c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val;}});
   > 
   > 
7. Hallo dezelfde aanpassingen maken met ~ \Views\WorkItems\Edit.cshtml.
8. Hallo `AadPicker` object is gedefinieerd in een script dat u nodig hebt tooadd tooyour project. Met de rechtermuisknop op Hallo ~\Scripts map, wijs het te**toevoegen**, en klik op **JavaScript-bestand**. Type `AadPickerLibrary` voor Hallo bestandsnaam en klik op **OK**.
9. Hallo-inhoud van kopiëren [hier](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) in ~ \Scripts\AadPickerLibrary.js.
   
   Hallo in Hallo script `AadPicker` object aanroepen [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) toosearch voor gebruikers en groepen die overeenkomen met de Hallo-invoer.  
10. Hallo wordt ook gebruikgemaakt van ~\Scripts\AadPickerLibrary.js [jQuery gebruikersinterface automatisch aanvullen widget](https://jqueryui.com/autocomplete/). U moet dus tooadd jQuery UI tooyour project. Met de rechtermuisknop op het project in en klik op **NuGet-pakketten beheren**.
11. Klik op Bladeren, in NuGet Package Manager Hallo, type **jquery-ui** in Hallo zoekbalk en klik op **jQuery.UI.Combined**.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/17-add-jquery-ui-nuget.png)
12. Klik in het rechterdeelvenster hello, **installeren**, klikt u vervolgens op **OK** tooproceed.
13. Open ~\App_Start\BundleConfig.cs en Hallo volgende gemarkeerde wijzigingen aanbrengen:  
    
    <pre class="prettyprint">
    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle(&quot;~/bundles/jquery&quot;).Include(
                    &quot;~/Scripts/jquery-{version}.js&quot;<mark>,
                    &quot;~/Scripts/jquery-ui-{version}.js&quot;,
                    &quot;~/Scripts/AadPickerLibrary.js&quot;</mark>));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/jqueryval&quot;).Include(
                    &quot;~/Scripts/jquery.validate*&quot;));
    
        // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
        // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
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
    
    Er zijn meer zodat manieren toomanage JavaScript en CSS-bestanden in uw app. Echter, ter vereenvoudiging NET gaat u toopiggyback op hello-pakketten die worden geladen met elke weergave.
14. Ten slotte in ~ \Global.asax, toevoegen van de volgende coderegel in Hallo Hallo `Application_Start()` methode. `Ctrl`+`.`op elke naming resolutie fout te corrigeren.
    
        AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.NameIdentifier;
    
    > [!NOTE]
    > U moet deze coderegel omdat Hallo standaard MVC-sjabloon gebruikt <code>[ValidateAntiForgeryToken]</code> decoration op een aantal acties Hallo. Vervaldatum toohello gedrag beschreven door [Brock Allen](https://twitter.com/BrockLAllen) op [MVC 4, AntiForgeryToken en Claims](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) uw HTTP POST ter voorkoming validatie van tokens kan mislukken omdat:
    > 
    > * Azure Active Directory verzendt geen Hallo http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider die wordt standaard door Hallo anti-vervalsingstoken vereist.
    > * Als Azure Active Directory directory gesynchroniseerd met AD FS, verzendt Hallo AD FS vertrouwen standaard geen Hallo http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider claim, maar u kunt AD FS toosend handmatig configureren Deze claim.
    > 
    > `ClaimTypes.NameIdentifies`Hiermee geeft u de claim Hallo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, die Azure Active Directory levert.  
    > 
    > 
15. Publiceer nu uw wijzigingen. Met de rechtermuisknop op uw project en klik op **publiceren**.
16. Klik op **instellingen**, zorg ervoor dat er is een verbinding tekenreeks tooyour SQL-Database, selecteert u **Database bijwerken** toomake Hallo wijzigingen in het schema voor het model en op **publiceren** .
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/18-publish-crud-changes.png)
17. Navigeer in Hallo browser toohttps: / /&lt;*appname*>.azurewebsites.net/workitems en klikt u op **nieuw**.
18. Klik in het Hallo **AssignedToName** vak. U ziet nu gebruikers en groepen van uw Azure Active Directory-tenant in een vervolgkeuzelijst. Typ toofilter of gebruik Hallo `Up` of `Down` sleutel of klik op tooselect Hallo gebruiker of groep. 
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/19-use-aadpicker.png)
19. Klik op **maken** toosave Hallo wijzigingen. Klik vervolgens op **bewerken** op Hallo gemaakt werk Hallo tooobserve item hetzelfde gedrag.

Gefeliciteerd, uitvoert u nu een line-of-business-app in Azure met toegang tot directory! Er is veel meer dat kunt u doen met Hallo Graph API. Zie [Azure AD Graph API-referentiemateriaal](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).

<a name="next"></a>

## <a name="next-step"></a>Volgende stap
Als u op rollen gebaseerde toegangsbeheer (RBAC) voor uw line-of-business-app in azure nodig hebt, raadpleegt u [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) voor een voorbeeld van hello Azure Active Directory-team. Hier ziet u hoe tooenable functies voor uw Azure Active Directory-toepassing, en vervolgens het autoriseren van gebruikers met Hallo `[Authorize]` decoration.

Als uw line-of-business-app moet tooon-premises gegevens toegankelijk zijn, Zie [toegang tot on-premises resources met behulp van hybride verbindingen in Azure App Service](web-sites-hybrid-connection-get-started.md).

<a name="bkmk_resources"></a>

## <a name="further-resources"></a>Meer bronnen
* [Verificatie en autorisatie in Azure App Service](../app-service/app-service-authentication-overview.md)
* [Verificatie met de on-premises Active Directory in uw app in Azure](web-sites-authentication-authorization.md)
* [Een line-of-business-app in Azure maken met AD FS-authenticatie](web-sites-dotnet-lob-application-adfs.md)
* [App Service Auth en hello Azure AD Graph API](https://cgillum.tech/2016/03/25/app-service-auth-aad-graph-api/)
* [Microsoft Azure Active Directory-voorbeelden en documentatie](https://github.com/AzureADSamples)
* [Azure Active Directory ondersteund Token en claimtypen](http://msdn.microsoft.com/library/azure/dn195587.aspx)
