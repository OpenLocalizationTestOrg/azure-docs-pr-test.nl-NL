---
title: aaaHow tooMake een telefonische oproep van Twilio (Java) | Microsoft Docs
description: Meer informatie over hoe een telefoon toomake aanroepen vanuit een webpagina met Twilio in een Java-toepassing in Azure.
services: 
documentationcenter: java
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 0381789e-e775-41a0-a784-294275192b1d
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 04fe5a78d431a79790dee3ca75c2b004aea4345d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomake-a-phone-call-using-twilio-in-a-java-application-on-azure"></a>Hoe tooMake een telefonische oproep met behulp van Twilio in een Java-toepassing in Azure
Hallo volgende voorbeeld ziet u hoe u kunt Twilio toomake een aanroep van een webpagina die wordt gehost in Azure. de resulterende toepassing Hello wordt Hallo gebruiker gevraagd om telefoongesprek waarden, zoals wordt weergegeven in de volgende schermopname Hallo.

![De aanroep van de Azure-formulier met Twilio en Java][twilio_java]

U moet toodo Hallo volgende toouse Hallo code in dit onderwerp:

1. Verkrijgen van een Twilio-account en verificatie token. tooget gestart met Twilio, evalueren prijzen op [http://www.twilio.com/pricing][twilio_pricing]. U kunt zich aanmelden op [https://www.twilio.com/try-twilio][try_twilio]. Zie voor meer informatie over Hallo API geleverd door Twilio [http://www.twilio.com/api][twilio_api].
2. Hallo Twilio JAR verkrijgen. Op [https://github.com/twilio/twilio-java][twilio_java_github], kunt u bronnen voor Hallo GitHub downloaden en uw eigen JAR maken of een vooraf samengestelde JAR (met of zonder afhankelijkheden) downloaden.
   Hallo-code in dit onderwerp is geschreven met behulp van vooraf samengestelde TwilioJava 3.3.8 met afhankelijkheden JAR Hallo.
3. Hallo JAR tooyour Java build path toevoegen.
4. Als u Eclipse toocreate deze Java-toepassing, opnemen Hallo Twilio JAR in uw implementatie toepassingsbestand (WAR) met behulp van de functie van Eclipse implementatie-assembly. Als u geen Eclipse toocreate deze Java-toepassing, zorg ervoor dat Hallo Twilio JAR is opgenomen in Hallo dezelfde Azure rol als klassepad voor uw toepassing en toegevoegde toohello van Java van uw toepassing.
5. Zorg ervoor dat uw keystore cacerts Hallo Equifax beveiligde CA-certificaat bevat met MD5 vingerafdruk 67:CB:9 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (Hallo seriële getal 35:DE:F4:CF en Hallo SHA1-vingerafdruk is D2:32:09:AD:23:D 3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A). Dit is Hallo-certificaat (certificeringsinstantie)-certificaat voor Hallo [https://api.twilio.com] [ twilio_api_service] -service, die wordt aangeroepen wanneer u Twilio APIs gebruiken. Zie voor meer informatie over het toevoegen van deze CA-certificaat tooyour JDK cacert store [toevoegen van een certificaat toohello Java CA-certificaatarchief][add_ca_cert].

Bovendien bekend bent met de informatie op Hallo [maken van een Hallo wereld wordt gebruikt door toepassing hello Azure Toolkit voor Eclipse][azure_java_eclipse_hello_world], of met andere technieken voor het hosten van Java-toepassingen in Azure als u Eclipse niet gebruikt, wordt sterk aanbevolen.

## <a name="create-a-web-form-for-making-a-call"></a>Maken van een webformulier voor het maken van een aanroep
Hallo volgende code toont hoe een web toocreate tooretrieve gebruikersgegevens voor het maken van een aanroep van vormen. Voor dit voorbeeld, een nieuw dynamic webproject met de naam **TwilioCloud**, is gemaakt, en **callform.jsp** is toegevoegd als een JSP-bestand.

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
        pageEncoding="ISO-8859-1" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Automated call form</title>
    </head>
    <body>
     <p>Fill in all fields and click <b>Make this call</b>.</p>
     <br/>
      <form action="makecall.jsp" method="post">
       <table>
         <tr>
           <td>To:</td>
           <td><input type="text" size=50 name="callTo" value="" />
           </td>
         </tr>
         <tr>
           <td>From:</td>
           <td><input type="text" size=50 name="callFrom" value="" />
           </td>
         </tr>
         <tr>
           <td>Call message:</td>
           <td><input type="text" size=400 name="callText" value="Hello. This is hello call text. Good bye." />
           </td>
         </tr>
         <tr>
           <td colspan=2><input type="submit" value="Make this call" />
           </td>
         </tr>
       </table>
     </form>
     <br/>
    </body>
    </html>

## <a name="create-hello-code-toomake-hello-call"></a>Hallo code toomake Hallo aanroep maken
Hallo volgende code, die wordt aangeroepen wanneer gebruiker Hallo Hallo formulier weergegeven door callform.jsp is voltooid, maakt aanroep het Hallo-bericht en genereert Hallo-aanroep. Voor dit voorbeeld Hallo JSP-bestand met de naam **makecall.jsp** en toohello is toegevoegd **TwilioCloud** project. (Gebruik uw Twilio-account en de verificatie-in plaats van de waarden van de tijdelijke aanduiding hello te toegewezen token**accountSID** en **authToken** in onderstaande Hallo-code.)

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    import="java.util.*"
    import="com.twilio.*"
    import="com.twilio.sdk.*"
    import="com.twilio.sdk.resource.factory.*"
    import="com.twilio.sdk.resource.instance.*"
    pageEncoding="ISO-8859-1" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Call processing happens here</title>
    </head>
    <body>
        <b>This is my make call page.</b><p/>
     <%
    try 
    {
         // Use your account SID and authentication token instead
         // of hello placeholders shown here.
         String accountSID = "your_twilio_account";
         String authToken = "your_twilio_authentication_token";

         // Instantiate an instance of hello Twilio client.     
         TwilioRestClient client;
         client = new TwilioRestClient(accountSID, authToken);

         // Retrieve hello account, used later tooretrieve hello CallFactory.
         Account account = client.getAccount();

         // Display hello client endpoint. 
         out.println("<p>Using Twilio endpoint " + client.getEndpoint() + ".</p>");

         // Display hello API version.
         String APIVERSION = TwilioRestClient.DEFAULT_VERSION;
         out.println("<p>Twilio client API version is " + APIVERSION + ".</p>");

         // Retrieve hello values entered by hello user.
         String callTo = request.getParameter("callTo");  
         // hello Outgoing Caller ID, used for hello From parameter,
         // must have previously been verified with Twilio.
         String callFrom = request.getParameter("callFrom");
         String userText = request.getParameter("callText");

         // Replace spaces in hello user's text with '%20', 
         // toomake hello text suitable for a URL.
         userText = userText.replace(" ", "%20");

         // Create a URL using hello Twilio message and hello user-entered text.
         String Url="http://twimlets.com/message";
         Url = Url + "?Message%5B0%5D=" + userText;

         // Display hello message URL.
         out.println("<p>");
         out.println("hello URL is " + Url);
         out.println("</p>");

         // Place hello call From, tooand URL values into a hash map. 
         HashMap<String, String> params = new HashMap<String, String>();
         params.put("From", callFrom);
         params.put("To", callTo);
         params.put("Url", Url);

         CallFactory callFactory = account.getCallFactory();
         Call call = callFactory.create(params);
         out.println("<p>Call status: " + call.getStatus()  + "</p>"); 
    } 
    catch (TwilioRestException e) 
    {
        out.println("<p>TwilioRestException encountered: " + e.getMessage() + "</p>");
        out.println("<p>StackTrace: " + e.getStackTrace().toString() + "</p>");
    }
    catch (Exception e) 
    {
        out.println("<p>Exception encountered: " + e.getMessage() + "");
        out.println("<p>StackTrace: " + e.getStackTrace().toString() + "</p>");
    }
    %>
    </body>
    </html>

Bovendien toomaking aanroep hello, makecall.jsp geeft Hallo Twilio-eindpunt, API-versie en de status van Hallo-aanroep. Een voorbeeld is de volgende schermopname Hallo:

![De aanroep van de Azure-antwoord met Twilio en Java][twilio_java_response]

## <a name="run-hello-application"></a>Hallo-toepassing uitvoeren
Volgende zijn stappen op hoog niveau toorun Hallo uw toepassing; Details voor deze stappen vindt u op [maken van een Hallo wereld wordt gebruikt door toepassing hello Azure Toolkit voor Eclipse][azure_java_eclipse_hello_world].

1. Exporteren van uw TwilioCloud WAR toohello Azure **approot** map. 
2. Wijzig **startup.cmd** toounzip uw WAR TwilioCloud.
3. Uw toepassing hello rekenemulator compileren.
4. Start uw implementatie in de Hallo rekenemulator.
5. Open een browser en voer **http://localhost:8080/TwilioCloud/callform.jsp**.
6. Voer waarden in de vorm hello, klikt u op **bellen**, en Ga naar Hallo resulteert in een makecall.jsp.

Wanneer u klaar toodeploy tooAzure bent, opnieuw moet compileren voor toohello implementatiecloud, tooAzure implementeren en uitvoeren http://*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp in Hallo browser (vervangen door de waarde voor *your_hosted_name*).

## <a name="next-steps"></a>Volgende stappen
Deze code is opgegeven tooshow u basisfunctionaliteit met Twilio in Java in Azure. Voordat u tooAzure in productie implementeert, kunt u tooadd meer foutafhandeling of andere onderdelen. Bijvoorbeeld:

* In plaats van een webformulier, Azure storage-blobs of SQL-Database toostore telefoonnummers te gebruiken en aanroepen van tekst. Zie voor meer informatie over het gebruik van Azure storage-blobs in Java [hoe tooUse Blob Storage-Service vanuit Java Hallo][howto_blob_storage_java]. Zie voor meer informatie over het gebruik van SQL-Database in Java [met behulp van SQL-Database in Java][howto_sql_azure_java].
* U kunt **RoleEnvironment.getConfigurationSettings** tooretrieve hello Twilio-account-ID en verificatie van uw implementatie-configuratie-instellingen, in plaats van hard-coding van Hallo waarden in makecall.jsp-token. Voor informatie over Hallo **RoleEnvironment** klasse, Zie [Using hello Azure Service Runtime-bibliotheek in JSP] [ azure_runtime_jsp] en hello Azure Service Runtime pakket documentatie op [http://dl.windowsazure.com/javadoc][azure_javadoc].
* Hallo makecall.jsp code wordt een Twilio-voorwaarde-URL, toegewezen [http://twimlets.com/message][twimlet_message_url], toohello **Url** variabele. Deze URL biedt een Twilio Markup Language (TwiML) antwoord dat informeert Twilio hoe tooproceed Hello aanroepen. Bijvoorbeeld, Hallo TwiML die wordt geretourneerd kunt bevatten een  **&lt;zeg&gt;**  term die resulteert in de tekst wordt gesproken toohello aanroep ontvanger. In plaats van Hallo geleverde Twilio-URL, kan u uw eigen service toorespond tooTwilio aanvraag; samenstellen Zie voor meer informatie [hoe tooUse Twilio voor spraak- en SMS-mogelijkheden in Java][howto_twilio_voice_sms_java]. Meer informatie over TwiML kan worden gevonden op [http://www.twilio.com/docs/api/twiml][twiml], en meer informatie over  **&lt;zeg&gt;**  en andere Twilio-termen kunnen worden gevonden op [http://www.twilio.com/docs/api/twiml/say][twilio_say].
* Hallo Twilio-richtlijnen voor beveiliging op lezen [https://www.twilio.com/docs/security][twilio_docs_security].

Zie voor meer informatie over Twilio [https://www.twilio.com/docs][twilio_docs].

## <a name="see-also"></a>Zie ook
* [Hoe tooUse Twilio voor spraak- en SMS-mogelijkheden in Java][howto_twilio_voice_sms_java]
* [Toevoegen van een certificaat toohello Java CA-certificaatarchief][add_ca_cert]

[twilio_pricing]: http://www.twilio.com/pricing
[try_twilio]: http://www.twilio.com/try-twilio
[twilio_api]: http://www.twilio.com/api
[verify_phone]: https://www.twilio.com/user/account/phone-numbers/verified#
[twilio_java_github]: http://github.com/twilio/twilio-java
[twimlet_message_url]: http://twimlets.com/message
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api_service]: http://api.twilio.com
[add_ca_cert]: java-add-certificate-ca-store.md
[azure_java_eclipse_hello_world]: http://msdn.microsoft.com/library/windowsazure/hh690944.aspx
[howto_twilio_voice_sms_java]: partner-twilio-java-how-to-use-voice-sms.md
[howto_blob_storage_java]: http://www.windowsazure.com/develop/java/how-to-guides/blob-storage/
[howto_sql_azure_java]: http://msdn.microsoft.com/library/windowsazure/hh749029.aspx
[azure_runtime_jsp]: http://msdn.microsoft.com/library/windowsazure/hh690948.aspx
[azure_javadoc]: http://dl.windowsazure.com/javadoc
[twilio_docs_security]: http://www.twilio.com/docs/security
[twilio_docs]: http://www.twilio.com/docs
[twilio_say]: http://www.twilio.com/docs/api/twiml/say
[twilio_java]: ./media/partner-twilio-java-phone-call-example/WA_TwilioJavaCallForm.jpg
[twilio_java_response]: ./media/partner-twilio-java-phone-call-example/WA_TwilioJavaMakeCall.jpg
