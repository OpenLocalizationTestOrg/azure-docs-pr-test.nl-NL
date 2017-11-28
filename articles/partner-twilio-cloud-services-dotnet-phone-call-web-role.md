---
title: aaaHow toomake een telefonische oproep van Twilio (.NET) | Microsoft Docs
description: Meer informatie over hoe toomake een telefonische oproep en verzend een SMS-met Hallo Twilio-API-service op Azure bericht. Codevoorbeelden geschreven in .NET.
services: 
documentationcenter: .net
author: devinrader
manager: timlt
editor: 
ms.assetid: 789185ad-69dc-4e9e-a936-42e0a25315c8
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/04/2016
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 857d89961c563a51fef944f4a72828036af79b43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomake-a-phone-call-using-twilio-in-a-web-role-on-azure"></a><span data-ttu-id="b534d-104">Hoe toomake een telefoon aanroepen met Twilio in een Webrol in Azure</span><span class="sxs-lookup"><span data-stu-id="b534d-104">How toomake a phone call using Twilio in a web role on Azure</span></span>
<span data-ttu-id="b534d-105">Deze handleiding wordt uitgelegd hoe toouse Twilio toomake een aanroep van een webpagina gehost in Azure.</span><span class="sxs-lookup"><span data-stu-id="b534d-105">This guide demonstrates how toouse Twilio toomake a call from a web page hosted in Azure.</span></span> <span data-ttu-id="b534d-106">de resulterende toepassing Hello wordt gevraagd Hallo gebruiker toomake een aanroep van Hello gegeven getal en het bericht, zoals wordt weergegeven in de volgende schermafbeelding Hallo.</span><span class="sxs-lookup"><span data-stu-id="b534d-106">hello resulting application prompts hello user toomake a call with hello given number and message, as shown in hello following screenshot.</span></span>

![De aanroep van de Azure-formulier met Twilio en ASP.NET][twilio_dotnet_basic_form]

## <span data-ttu-id="b534d-108"><a name="twilio-prereqs"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="b534d-108"><a name="twilio-prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="b534d-109">U moet toodo Hallo volgende toouse Hallo code in dit onderwerp:</span><span class="sxs-lookup"><span data-stu-id="b534d-109">You will need toodo hello following toouse hello code in this topic:</span></span>

1. <span data-ttu-id="b534d-110">Verkrijgen van een Twilio-account en verificatie-token van Hallo [Twilio Console][twilio_console].</span><span class="sxs-lookup"><span data-stu-id="b534d-110">Acquire a Twilio account and authentication token from hello [Twilio Console][twilio_console].</span></span> <span data-ttu-id="b534d-111">tooget gestart met Twilio, aanmelding bij [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="b534d-111">tooget started with Twilio, sign up at [https://www.twilio.com/try-twilio][try_twilio].</span></span> <span data-ttu-id="b534d-112">U kunt evalueren prijzen op [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="b534d-112">You can evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="b534d-113">Zie voor meer informatie over Hallo API geleverd door Twilio [http://www.twilio.com/voice/api][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="b534d-113">For information about hello API provided by Twilio, see [http://www.twilio.com/voice/api][twilio_api].</span></span>
2. <span data-ttu-id="b534d-114">Hallo toevoegen *Twilio .NET-bibliotheek* tooyour Webrol.</span><span class="sxs-lookup"><span data-stu-id="b534d-114">Add hello *Twilio .NET libary* tooyour web role.</span></span> <span data-ttu-id="b534d-115">Zie **tooadd hello Twilio-bibliotheken tooyour webrolproject**verderop in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="b534d-115">See **tooadd hello Twilio libraries tooyour web role project**, later in this topic.</span></span>

<span data-ttu-id="b534d-116">U moet bekend bent met het maken van een eenvoudige [Webrol in Azure][azure_webroles_get_started].</span><span class="sxs-lookup"><span data-stu-id="b534d-116">You should be familiar with creating a basic [Web Role on Azure][azure_webroles_get_started].</span></span>

## <span data-ttu-id="b534d-117"><a name="howtocreateform"></a>Procedure: een webformulier voor het maken van een aanroep maken</span><span class="sxs-lookup"><span data-stu-id="b534d-117"><a name="howtocreateform"></a>How to: Create a web form for making a call</span></span>
<span data-ttu-id="b534d-118"><a id="use_nuget"></a>tooadd hello Twilio-bibliotheken tooyour webrolproject:</span><span class="sxs-lookup"><span data-stu-id="b534d-118"><a id="use_nuget"></a>tooadd hello Twilio libraries tooyour web role project:</span></span>

1. <span data-ttu-id="b534d-119">Open uw oplossing in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b534d-119">Open your solution in Visual Studio.</span></span>
2. <span data-ttu-id="b534d-120">Met de rechtermuisknop op **verwijzingen**.</span><span class="sxs-lookup"><span data-stu-id="b534d-120">Right-click **References**.</span></span>
3. <span data-ttu-id="b534d-121">Klik op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="b534d-121">Click **Manage NuGet Packages**.</span></span>
4. <span data-ttu-id="b534d-122">Klik op **Online**.</span><span class="sxs-lookup"><span data-stu-id="b534d-122">Click **Online**.</span></span>
5. <span data-ttu-id="b534d-123">Typ in de online zoekvak hello, *twilio*.</span><span class="sxs-lookup"><span data-stu-id="b534d-123">In hello search online box, type *twilio*.</span></span>
6. <span data-ttu-id="b534d-124">Klik op **installeren** op Hallo Twilio-pakket.</span><span class="sxs-lookup"><span data-stu-id="b534d-124">Click **Install** on hello Twilio package.</span></span>

<span data-ttu-id="b534d-125">Hallo volgende code toont hoe een web toocreate tooretrieve gebruikersgegevens voor het maken van een aanroep van vormen.</span><span class="sxs-lookup"><span data-stu-id="b534d-125">hello following code shows how toocreate a web form tooretrieve user data for making a call.</span></span> <span data-ttu-id="b534d-126">In dit voorbeeld wordt een ASP.NET-Webrol met de naam **TwilioCloud** wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b534d-126">In this example, an ASP.NET Web Role named **TwilioCloud** is created.</span></span>

```aspx
<%@ Page Title="Home Page" Language="C#" MasterPageFile="~/Site.master"
    AutoEventWireup="true" CodeBehind="Default.aspx.cs"
    Inherits="WebRole1._Default" %>

<asp:Content ID="HeaderContent" runat="server" ContentPlaceHolderID="HeadContent">
</asp:Content>
<asp:Content ID="BodyContent" runat="server" ContentPlaceHolderID="MainContent">
    <div>
        <asp:BulletedList ID="varDisplay" runat="server" BulletStyle="NotSet">
        </asp:BulletedList>
    </div>
    <div>
        <p>Fill in all fields and click <b>Make this call</b>.</p>
        <div>
            To:<br /><asp:TextBox ID="toNumber" runat="server" /><br /><br />
            Message:<br /><asp:TextBox ID="message" runat="server" /><br /><br />
            <asp:Button ID="callpage" runat="server" Text="Make this call"
                onclick="callpage_Click" />
        </div>
    </div>
</asp:Content>
```

## <span data-ttu-id="b534d-127"><a id="howtocreatecode"></a>Hoe: Hallo code toomake Hallo aanroep maken</span><span class="sxs-lookup"><span data-stu-id="b534d-127"><a id="howtocreatecode"></a>How to: Create hello code toomake hello call</span></span>
<span data-ttu-id="b534d-128">Hallo volgende code, die wordt aangeroepen wanneer gebruiker Hallo Hallo formulier is voltooid, maakt aanroep het Hallo-bericht en genereert Hallo-aanroep.</span><span class="sxs-lookup"><span data-stu-id="b534d-128">hello following code, which is called when hello user completes hello form, creates hello call message and generates hello call.</span></span> <span data-ttu-id="b534d-129">In dit voorbeeld Hallo code uitvoeren in Hallo onclick gebeurtenis-handler van Hallo knop op Hallo formulier.</span><span class="sxs-lookup"><span data-stu-id="b534d-129">In this example, hello code is run in hello onclick event handler of hello button on hello form.</span></span> <span data-ttu-id="b534d-130">(Gebruik uw Twilio-account en de verificatie-in plaats van de waarden van de tijdelijke aanduiding hello te toegewezen token`accountSID` en `authToken` in onderstaande Hallo-code.)</span><span class="sxs-lookup"><span data-stu-id="b534d-130">(Use your Twilio account and authentication token instead of hello placeholder values assigned too`accountSID` and `authToken` in hello code below.)</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using Twilio;
using Twilio.Http;
using Twilio.Types;
using Twilio.Rest.Api.V2010;

namespace WebRole1
{
    public partial class _Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {

        }

        protected void callpage_Click(object sender, EventArgs e)
        {
            // Call porcessing happens here.

            // Use your account SID and authentication token instead of
            // hello placeholders shown here.
            var accountSID = "ACNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN";
            var authToken =  "NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN";

            // Instantiate an instance of hello Twilio client.
            TwilioClient.Init(accountSID, authToken);

            // Retrieve hello account, used later tooretrieve the
            var account = AccountResource.Fetch(accountSID);

            this.varDisplay.Items.Clear();

            if (this.toNumber.Text == "" || this.message.Text == "")
            {
                this.varDisplay.Items.Add(
                        "You must enter a phone number and a message.");
            }
            else
            {
                // Retrieve hello values entered by hello user.
                var too= PhoneNumber(this.toNumber.Text);
                var from = new PhoneNumber("+14155992671");
                var myMessage = this.message.Text;

                // Create a URL using hello Twilio message and hello user-entered
                // text. You must replace spaces in hello user's text with '%20'
                // toomake hello text suitable for a URL.
                var url = $"http://twimlets.com/message?Message%5B0%5D={myMessage.Replace(" ", "%20")}";
                var twimlUri = new Uri(url);

                // Display hello endpoint, API version, and hello URL for hello message.
                this.varDisplay.Items.Add($"Using Twilio endpoint {
                }");
                this.varDisplay.Items.Add($"Twilioclient API Version is {apiVersion}");
                this.varDisplay.Items.Add($"hello URL is {url}");

                // Place hello call.
                var call = CallResource.create(to, from, url: twimlUri);
                this.varDisplay.Items.Add("Call status: " + call.Status);
            }
        }
    }
}
```

<span data-ttu-id="b534d-131">Hallo-aanroep is uitgevoerd en Hallo Twilio-eindpunt, API-versie en Hallo aanroep status worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b534d-131">hello call is made, and hello Twilio endpoint, API version, and hello call status are displayed.</span></span> <span data-ttu-id="b534d-132">Hallo volgende Schermafbeelding toont uitvoer uit een steekproef die worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b534d-132">hello following screenshot shows output from a sample run.</span></span>

![De aanroep van de Azure-antwoord met Twilio en ASP.NET][twilio_dotnet_basic_form_output]

<span data-ttu-id="b534d-134">Meer informatie over TwiML kan worden gevonden op [http://www.twilio.com/docs/api/twiml][twiml].</span><span class="sxs-lookup"><span data-stu-id="b534d-134">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml].</span></span> <span data-ttu-id="b534d-135">Meer informatie over &lt;zeg&gt; en andere Twilio-termen kunnen worden gevonden op [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="b534d-135">More information about &lt;Say&gt; and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>

## <span data-ttu-id="b534d-136"><a id="nextsteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b534d-136"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="b534d-137">Deze code is opgegeven tooshow u basisfunctionaliteit met Twilio in een ASP.NET-Webrol in Azure.</span><span class="sxs-lookup"><span data-stu-id="b534d-137">This code was provided tooshow you basic functionality using Twilio in an ASP.NET web role on Azure.</span></span> <span data-ttu-id="b534d-138">Voordat u tooAzure in productie implementeert, kunt u tooadd meer foutafhandeling of andere onderdelen.</span><span class="sxs-lookup"><span data-stu-id="b534d-138">Before deploying tooAzure in production, you may want tooadd more error handling or other features.</span></span> <span data-ttu-id="b534d-139">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b534d-139">For example:</span></span>

* <span data-ttu-id="b534d-140">In plaats van een webformulier, Azure Blob-opslag of een Azure SQL Database-exemplaar toostore-telefoonnummers te gebruiken en aanroepen van tekst.</span><span class="sxs-lookup"><span data-stu-id="b534d-140">Instead of using a web form, you could use Azure Blob storage or an Azure SQL Database instance toostore phone numbers and call text.</span></span> <span data-ttu-id="b534d-141">Zie voor meer informatie over het gebruik van de Blobs in Azure [hoe toouse hello Azure Blob storage-service in .NET][howto_blob_storage_dotnet].</span><span class="sxs-lookup"><span data-stu-id="b534d-141">For information about using Blobs in Azure, see [How toouse hello Azure Blob storage service in .NET][howto_blob_storage_dotnet].</span></span> <span data-ttu-id="b534d-142">Zie voor meer informatie over het gebruik van SQL-Database [hoe toouse Azure SQL-Database in .NET-toepassingen][howto_sql_azure_dotnet].</span><span class="sxs-lookup"><span data-stu-id="b534d-142">For information about using SQL Database, see [How toouse Azure SQL Database in .NET applications][howto_sql_azure_dotnet].</span></span>
* <span data-ttu-id="b534d-143">U kunt `RoleEnvironment.getConfigurationSettings` tooretrieve hello Twilio-account-ID en de verificatie-token van uw implementatie-configuratie-instellingen, in plaats van hard-coding van Hallo waarden in het formulier.</span><span class="sxs-lookup"><span data-stu-id="b534d-143">You could use `RoleEnvironment.getConfigurationSettings` tooretrieve hello Twilio account ID and authentication token from your deployment's configuration settings, instead of hard-coding hello values in your form.</span></span> <span data-ttu-id="b534d-144">Voor informatie over Hallo `RoleEnvironment` klasse, Zie [Microsoft.WindowsAzure.ServiceRuntime Namespace][azure_runtime_ref_dotnet].</span><span class="sxs-lookup"><span data-stu-id="b534d-144">For information about hello `RoleEnvironment` class, see [Microsoft.WindowsAzure.ServiceRuntime Namespace][azure_runtime_ref_dotnet].</span></span>
* <span data-ttu-id="b534d-145">Hallo Twilio-richtlijnen voor beveiliging op lezen [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="b534d-145">Read hello Twilio Security Guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>
* <span data-ttu-id="b534d-146">Meer informatie over Twilio op [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="b534d-146">Learn more about Twilio at [https://www.twilio.com/docs][twilio_docs].</span></span>

## <span data-ttu-id="b534d-147"><a name="seealso"></a>Zie ook</span><span class="sxs-lookup"><span data-stu-id="b534d-147"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="b534d-148">Hoe toouse Twilio voor spraak- en SMS-mogelijkheden van Azure</span><span class="sxs-lookup"><span data-stu-id="b534d-148">How toouse Twilio for Voice and SMS capabilities from Azure</span></span>](twilio-dotnet-how-to-use-for-voice-sms.md)

[twilio_console]: https://www.twilio.com/console
[twilio_pricing]: http://www.twilio.com/pricing
[try_twilio]: http://www.twilio.com/try-twilio
[twilio_api]: http://www.twilio.com/voice/api
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified

[twilio_dotnet_basic_form]: ./media/partner-twilio-cloud-services-dotnet-phone-call-web-role/WA_twilio_dotnet_basic_form.png
[twilio_dotnet_basic_form_output]: ./media/partner-twilio-cloud-services-dotnet-phone-call-web-role/WA_twilio_dotnet_basic_form_output.png

[twiml]: http://www.twilio.com/docs/api/twiml



[howto_twilio_voice_sms_dotnet]: /develop/net/how-to-guides/twilio/

[howto_blob_storage_dotnet]: https://www.windowsazure.com/develop/net/how-to-guides/blob-storage/

[howto_sql_azure_dotnet]: https://www.windowsazure.com/develop/net/how-to-guides/sql-database/


[twilio_docs_security]: http://www.twilio.com/docs/security
[twilio_docs]: http://www.twilio.com/docs
[twilio_say]: http://www.twilio.com/docs/api/twiml/say


[azure_runtime_ref_dotnet]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.aspx
[azure_webroles_get_started]: https://docs.microsoft.com/en-us/azure/cloud-services/cloud-services-dotnet-get-started
