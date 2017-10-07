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
# <a name="how-toomake-a-phone-call-using-twilio-in-a-web-role-on-azure"></a>Hoe toomake een telefoon aanroepen met Twilio in een Webrol in Azure
Deze handleiding wordt uitgelegd hoe toouse Twilio toomake een aanroep van een webpagina gehost in Azure. de resulterende toepassing Hello wordt gevraagd Hallo gebruiker toomake een aanroep van Hello gegeven getal en het bericht, zoals wordt weergegeven in de volgende schermafbeelding Hallo.

![De aanroep van de Azure-formulier met Twilio en ASP.NET][twilio_dotnet_basic_form]

## <a name="twilio-prereqs"></a>Vereisten
U moet toodo Hallo volgende toouse Hallo code in dit onderwerp:

1. Verkrijgen van een Twilio-account en verificatie-token van Hallo [Twilio Console][twilio_console]. tooget gestart met Twilio, aanmelding bij [https://www.twilio.com/try-twilio][try_twilio]. U kunt evalueren prijzen op [http://www.twilio.com/pricing][twilio_pricing]. Zie voor meer informatie over Hallo API geleverd door Twilio [http://www.twilio.com/voice/api][twilio_api].
2. Hallo toevoegen *Twilio .NET-bibliotheek* tooyour Webrol. Zie **tooadd hello Twilio-bibliotheken tooyour webrolproject**verderop in dit onderwerp.

U moet bekend bent met het maken van een eenvoudige [Webrol in Azure][azure_webroles_get_started].

## <a name="howtocreateform"></a>Procedure: een webformulier voor het maken van een aanroep maken
<a id="use_nuget"></a>tooadd hello Twilio-bibliotheken tooyour webrolproject:

1. Open uw oplossing in Visual Studio.
2. Met de rechtermuisknop op **verwijzingen**.
3. Klik op **NuGet-pakketten beheren**.
4. Klik op **Online**.
5. Typ in de online zoekvak hello, *twilio*.
6. Klik op **installeren** op Hallo Twilio-pakket.

Hallo volgende code toont hoe een web toocreate tooretrieve gebruikersgegevens voor het maken van een aanroep van vormen. In dit voorbeeld wordt een ASP.NET-Webrol met de naam **TwilioCloud** wordt gemaakt.

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

## <a id="howtocreatecode"></a>Hoe: Hallo code toomake Hallo aanroep maken
Hallo volgende code, die wordt aangeroepen wanneer gebruiker Hallo Hallo formulier is voltooid, maakt aanroep het Hallo-bericht en genereert Hallo-aanroep. In dit voorbeeld Hallo code uitvoeren in Hallo onclick gebeurtenis-handler van Hallo knop op Hallo formulier. (Gebruik uw Twilio-account en de verificatie-in plaats van de waarden van de tijdelijke aanduiding hello te toegewezen token`accountSID` en `authToken` in onderstaande Hallo-code.)

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

Hallo-aanroep is uitgevoerd en Hallo Twilio-eindpunt, API-versie en Hallo aanroep status worden weergegeven. Hallo volgende Schermafbeelding toont uitvoer uit een steekproef die worden uitgevoerd.

![De aanroep van de Azure-antwoord met Twilio en ASP.NET][twilio_dotnet_basic_form_output]

Meer informatie over TwiML kan worden gevonden op [http://www.twilio.com/docs/api/twiml][twiml]. Meer informatie over &lt;zeg&gt; en andere Twilio-termen kunnen worden gevonden op [http://www.twilio.com/docs/api/twiml/say][twilio_say].

## <a id="nextsteps"></a>Volgende stappen
Deze code is opgegeven tooshow u basisfunctionaliteit met Twilio in een ASP.NET-Webrol in Azure. Voordat u tooAzure in productie implementeert, kunt u tooadd meer foutafhandeling of andere onderdelen. Bijvoorbeeld:

* In plaats van een webformulier, Azure Blob-opslag of een Azure SQL Database-exemplaar toostore-telefoonnummers te gebruiken en aanroepen van tekst. Zie voor meer informatie over het gebruik van de Blobs in Azure [hoe toouse hello Azure Blob storage-service in .NET][howto_blob_storage_dotnet]. Zie voor meer informatie over het gebruik van SQL-Database [hoe toouse Azure SQL-Database in .NET-toepassingen][howto_sql_azure_dotnet].
* U kunt `RoleEnvironment.getConfigurationSettings` tooretrieve hello Twilio-account-ID en de verificatie-token van uw implementatie-configuratie-instellingen, in plaats van hard-coding van Hallo waarden in het formulier. Voor informatie over Hallo `RoleEnvironment` klasse, Zie [Microsoft.WindowsAzure.ServiceRuntime Namespace][azure_runtime_ref_dotnet].
* Hallo Twilio-richtlijnen voor beveiliging op lezen [https://www.twilio.com/docs/security][twilio_docs_security].
* Meer informatie over Twilio op [https://www.twilio.com/docs][twilio_docs].

## <a name="seealso"></a>Zie ook
* [Hoe toouse Twilio voor spraak- en SMS-mogelijkheden van Azure](twilio-dotnet-how-to-use-for-voice-sms.md)

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
