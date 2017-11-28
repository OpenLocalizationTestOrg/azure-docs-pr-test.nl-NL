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
# <a name="how-toomake-a-phone-call-using-twilio-in-a-java-application-on-azure"></a><span data-ttu-id="5133b-103">Hoe tooMake een telefonische oproep met behulp van Twilio in een Java-toepassing in Azure</span><span class="sxs-lookup"><span data-stu-id="5133b-103">How tooMake a Phone Call Using Twilio in a Java Application on Azure</span></span>
<span data-ttu-id="5133b-104">Hallo volgende voorbeeld ziet u hoe u kunt Twilio toomake een aanroep van een webpagina die wordt gehost in Azure.</span><span class="sxs-lookup"><span data-stu-id="5133b-104">hello following example shows you how you can use Twilio toomake a call from a web page hosted in Azure.</span></span> <span data-ttu-id="5133b-105">de resulterende toepassing Hello wordt Hallo gebruiker gevraagd om telefoongesprek waarden, zoals wordt weergegeven in de volgende schermopname Hallo.</span><span class="sxs-lookup"><span data-stu-id="5133b-105">hello resulting application will prompt hello user for phone call values, as shown in hello following screen shot.</span></span>

![De aanroep van de Azure-formulier met Twilio en Java][twilio_java]

<span data-ttu-id="5133b-107">U moet toodo Hallo volgende toouse Hallo code in dit onderwerp:</span><span class="sxs-lookup"><span data-stu-id="5133b-107">You'll need toodo hello following toouse hello code in this topic:</span></span>

1. <span data-ttu-id="5133b-108">Verkrijgen van een Twilio-account en verificatie token.</span><span class="sxs-lookup"><span data-stu-id="5133b-108">Acquire a Twilio account and authentication token.</span></span> <span data-ttu-id="5133b-109">tooget gestart met Twilio, evalueren prijzen op [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="5133b-109">tooget started with Twilio, evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="5133b-110">U kunt zich aanmelden op [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="5133b-110">You can sign up at [https://www.twilio.com/try-twilio][try_twilio].</span></span> <span data-ttu-id="5133b-111">Zie voor meer informatie over Hallo API geleverd door Twilio [http://www.twilio.com/api][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="5133b-111">For information about hello API provided by Twilio, see [http://www.twilio.com/api][twilio_api].</span></span>
2. <span data-ttu-id="5133b-112">Hallo Twilio JAR verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="5133b-112">Obtain hello Twilio JAR.</span></span> <span data-ttu-id="5133b-113">Op [https://github.com/twilio/twilio-java][twilio_java_github], kunt u bronnen voor Hallo GitHub downloaden en uw eigen JAR maken of een vooraf samengestelde JAR (met of zonder afhankelijkheden) downloaden.</span><span class="sxs-lookup"><span data-stu-id="5133b-113">At [https://github.com/twilio/twilio-java][twilio_java_github], you can download hello GitHub sources and create your own JAR, or download a pre-built JAR (with or without dependencies).</span></span>
   <span data-ttu-id="5133b-114">Hallo-code in dit onderwerp is geschreven met behulp van vooraf samengestelde TwilioJava 3.3.8 met afhankelijkheden JAR Hallo.</span><span class="sxs-lookup"><span data-stu-id="5133b-114">hello code in this topic was written using hello pre-built TwilioJava-3.3.8-with-dependencies JAR.</span></span>
3. <span data-ttu-id="5133b-115">Hallo JAR tooyour Java build path toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5133b-115">Add hello JAR tooyour Java build path.</span></span>
4. <span data-ttu-id="5133b-116">Als u Eclipse toocreate deze Java-toepassing, opnemen Hallo Twilio JAR in uw implementatie toepassingsbestand (WAR) met behulp van de functie van Eclipse implementatie-assembly.</span><span class="sxs-lookup"><span data-stu-id="5133b-116">If you are using Eclipse toocreate this Java application, include hello Twilio JAR in your application deployment file (WAR) using Eclipse's deployment assembly feature.</span></span> <span data-ttu-id="5133b-117">Als u geen Eclipse toocreate deze Java-toepassing, zorg ervoor dat Hallo Twilio JAR is opgenomen in Hallo dezelfde Azure rol als klassepad voor uw toepassing en toegevoegde toohello van Java van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="5133b-117">If you are not using Eclipse toocreate this Java application, ensure hello Twilio JAR is included within hello same Azure role as your Java application, and added toohello class path of your application.</span></span>
5. <span data-ttu-id="5133b-118">Zorg ervoor dat uw keystore cacerts Hallo Equifax beveiligde CA-certificaat bevat met MD5 vingerafdruk 67:CB:9 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (Hallo seriële getal 35:DE:F4:CF en Hallo SHA1-vingerafdruk is D2:32:09:AD:23:D 3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A).</span><span class="sxs-lookup"><span data-stu-id="5133b-118">Ensure your cacerts keystore contains hello Equifax Secure Certificate Authority certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (hello serial number is 35:DE:F4:CF and hello SHA1 fingerprint is D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span></span> <span data-ttu-id="5133b-119">Dit is Hallo-certificaat (certificeringsinstantie)-certificaat voor Hallo [https://api.twilio.com] [ twilio_api_service] -service, die wordt aangeroepen wanneer u Twilio APIs gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5133b-119">This is hello certificate authority (CA) certificate for hello [https://api.twilio.com][twilio_api_service] service, which is called when you use Twilio APIs.</span></span> <span data-ttu-id="5133b-120">Zie voor meer informatie over het toevoegen van deze CA-certificaat tooyour JDK cacert store [toevoegen van een certificaat toohello Java CA-certificaatarchief][add_ca_cert].</span><span class="sxs-lookup"><span data-stu-id="5133b-120">For information about adding this CA certificate tooyour JDK's cacert store, see [Adding a Certificate toohello Java CA Certificate Store][add_ca_cert].</span></span>

<span data-ttu-id="5133b-121">Bovendien bekend bent met de informatie op Hallo [maken van een Hallo wereld wordt gebruikt door toepassing hello Azure Toolkit voor Eclipse][azure_java_eclipse_hello_world], of met andere technieken voor het hosten van Java-toepassingen in Azure als u Eclipse niet gebruikt, wordt sterk aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="5133b-121">Additionally, familiarity with hello information at [Creating a Hello World Application Using hello Azure Toolkit for Eclipse][azure_java_eclipse_hello_world], or with other techniques for hosting Java applications in Azure if you are not using Eclipse, is highly recommended.</span></span>

## <a name="create-a-web-form-for-making-a-call"></a><span data-ttu-id="5133b-122">Maken van een webformulier voor het maken van een aanroep</span><span class="sxs-lookup"><span data-stu-id="5133b-122">Create a web form for making a call</span></span>
<span data-ttu-id="5133b-123">Hallo volgende code toont hoe een web toocreate tooretrieve gebruikersgegevens voor het maken van een aanroep van vormen.</span><span class="sxs-lookup"><span data-stu-id="5133b-123">hello following code shows how toocreate a web form tooretrieve user data for making a call.</span></span> <span data-ttu-id="5133b-124">Voor dit voorbeeld, een nieuw dynamic webproject met de naam **TwilioCloud**, is gemaakt, en **callform.jsp** is toegevoegd als een JSP-bestand.</span><span class="sxs-lookup"><span data-stu-id="5133b-124">For purposes of this example, a new dynamic web project, named **TwilioCloud**, was created, and **callform.jsp** was added as a JSP file.</span></span>

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

## <a name="create-hello-code-toomake-hello-call"></a><span data-ttu-id="5133b-125">Hallo code toomake Hallo aanroep maken</span><span class="sxs-lookup"><span data-stu-id="5133b-125">Create hello code toomake hello call</span></span>
<span data-ttu-id="5133b-126">Hallo volgende code, die wordt aangeroepen wanneer gebruiker Hallo Hallo formulier weergegeven door callform.jsp is voltooid, maakt aanroep het Hallo-bericht en genereert Hallo-aanroep.</span><span class="sxs-lookup"><span data-stu-id="5133b-126">hello following code, which is called when hello user completes hello form displayed by callform.jsp, creates hello call message and generates hello call.</span></span> <span data-ttu-id="5133b-127">Voor dit voorbeeld Hallo JSP-bestand met de naam **makecall.jsp** en toohello is toegevoegd **TwilioCloud** project.</span><span class="sxs-lookup"><span data-stu-id="5133b-127">For purposes of this example, hello JSP file is named **makecall.jsp** and was added toohello **TwilioCloud** project.</span></span> <span data-ttu-id="5133b-128">(Gebruik uw Twilio-account en de verificatie-in plaats van de waarden van de tijdelijke aanduiding hello te toegewezen token**accountSID** en **authToken** in onderstaande Hallo-code.)</span><span class="sxs-lookup"><span data-stu-id="5133b-128">(Use your Twilio account and authentication token instead of hello placeholder values assigned too**accountSID** and **authToken** in hello code below.)</span></span>

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

<span data-ttu-id="5133b-129">Bovendien toomaking aanroep hello, makecall.jsp geeft Hallo Twilio-eindpunt, API-versie en de status van Hallo-aanroep.</span><span class="sxs-lookup"><span data-stu-id="5133b-129">In addition toomaking hello call, makecall.jsp displays hello Twilio endpoint, API version, and hello call status.</span></span> <span data-ttu-id="5133b-130">Een voorbeeld is de volgende schermopname Hallo:</span><span class="sxs-lookup"><span data-stu-id="5133b-130">An example is hello following screen shot:</span></span>

![De aanroep van de Azure-antwoord met Twilio en Java][twilio_java_response]

## <a name="run-hello-application"></a><span data-ttu-id="5133b-132">Hallo-toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="5133b-132">Run hello application</span></span>
<span data-ttu-id="5133b-133">Volgende zijn stappen op hoog niveau toorun Hallo uw toepassing; Details voor deze stappen vindt u op [maken van een Hallo wereld wordt gebruikt door toepassing hello Azure Toolkit voor Eclipse][azure_java_eclipse_hello_world].</span><span class="sxs-lookup"><span data-stu-id="5133b-133">Following are hello high-level steps toorun your application; details for these steps can be found at [Creating a Hello World Application Using hello Azure Toolkit for Eclipse][azure_java_eclipse_hello_world].</span></span>

1. <span data-ttu-id="5133b-134">Exporteren van uw TwilioCloud WAR toohello Azure **approot** map.</span><span class="sxs-lookup"><span data-stu-id="5133b-134">Export your TwilioCloud WAR toohello Azure **approot** folder.</span></span> 
2. <span data-ttu-id="5133b-135">Wijzig **startup.cmd** toounzip uw WAR TwilioCloud.</span><span class="sxs-lookup"><span data-stu-id="5133b-135">Modify **startup.cmd** toounzip your TwilioCloud WAR.</span></span>
3. <span data-ttu-id="5133b-136">Uw toepassing hello rekenemulator compileren.</span><span class="sxs-lookup"><span data-stu-id="5133b-136">Compile your application for hello compute emulator.</span></span>
4. <span data-ttu-id="5133b-137">Start uw implementatie in de Hallo rekenemulator.</span><span class="sxs-lookup"><span data-stu-id="5133b-137">Start your deployment in hello compute emulator.</span></span>
5. <span data-ttu-id="5133b-138">Open een browser en voer **http://localhost:8080/TwilioCloud/callform.jsp**.</span><span class="sxs-lookup"><span data-stu-id="5133b-138">Open a browser, and run **http://localhost:8080/TwilioCloud/callform.jsp**.</span></span>
6. <span data-ttu-id="5133b-139">Voer waarden in de vorm hello, klikt u op **bellen**, en Ga naar Hallo resulteert in een makecall.jsp.</span><span class="sxs-lookup"><span data-stu-id="5133b-139">Enter values in hello form, click **Make this call**, and then see hello results in makecall.jsp.</span></span>

<span data-ttu-id="5133b-140">Wanneer u klaar toodeploy tooAzure bent, opnieuw moet compileren voor toohello implementatiecloud, tooAzure implementeren en uitvoeren http://*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp in Hallo browser (vervangen door de waarde voor *your_hosted_name*).</span><span class="sxs-lookup"><span data-stu-id="5133b-140">When you are ready toodeploy tooAzure, recompile for deployment toohello cloud, deploy tooAzure, and run http://*your_hosted_name*.cloudapp.net/TwilioCloud/callform.jsp in hello browser (substitute your value for *your_hosted_name*).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5133b-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5133b-141">Next steps</span></span>
<span data-ttu-id="5133b-142">Deze code is opgegeven tooshow u basisfunctionaliteit met Twilio in Java in Azure.</span><span class="sxs-lookup"><span data-stu-id="5133b-142">This code was provided tooshow you basic functionality using Twilio in Java on Azure.</span></span> <span data-ttu-id="5133b-143">Voordat u tooAzure in productie implementeert, kunt u tooadd meer foutafhandeling of andere onderdelen.</span><span class="sxs-lookup"><span data-stu-id="5133b-143">Before deploying tooAzure in production, you may want tooadd more error handling or other features.</span></span> <span data-ttu-id="5133b-144">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="5133b-144">For example:</span></span>

* <span data-ttu-id="5133b-145">In plaats van een webformulier, Azure storage-blobs of SQL-Database toostore telefoonnummers te gebruiken en aanroepen van tekst.</span><span class="sxs-lookup"><span data-stu-id="5133b-145">Instead of using a web form, you could use Azure storage blobs or SQL Database toostore phone numbers and call text.</span></span> <span data-ttu-id="5133b-146">Zie voor meer informatie over het gebruik van Azure storage-blobs in Java [hoe tooUse Blob Storage-Service vanuit Java Hallo][howto_blob_storage_java].</span><span class="sxs-lookup"><span data-stu-id="5133b-146">For information about using Azure storage blobs in Java, see [How tooUse hello Blob Storage Service from Java][howto_blob_storage_java].</span></span> <span data-ttu-id="5133b-147">Zie voor meer informatie over het gebruik van SQL-Database in Java [met behulp van SQL-Database in Java][howto_sql_azure_java].</span><span class="sxs-lookup"><span data-stu-id="5133b-147">For information about using SQL Database in Java, see [Using SQL Database in Java][howto_sql_azure_java].</span></span>
* <span data-ttu-id="5133b-148">U kunt **RoleEnvironment.getConfigurationSettings** tooretrieve hello Twilio-account-ID en verificatie van uw implementatie-configuratie-instellingen, in plaats van hard-coding van Hallo waarden in makecall.jsp-token.</span><span class="sxs-lookup"><span data-stu-id="5133b-148">You could use **RoleEnvironment.getConfigurationSettings** tooretrieve hello Twilio account ID and authentication token from your deployment's configuration settings, instead of hard-coding hello values in makecall.jsp.</span></span> <span data-ttu-id="5133b-149">Voor informatie over Hallo **RoleEnvironment** klasse, Zie [Using hello Azure Service Runtime-bibliotheek in JSP] [ azure_runtime_jsp] en hello Azure Service Runtime pakket documentatie op [http://dl.windowsazure.com/javadoc][azure_javadoc].</span><span class="sxs-lookup"><span data-stu-id="5133b-149">For information about hello **RoleEnvironment** class, see [Using hello Azure Service Runtime Library in JSP][azure_runtime_jsp] and hello Azure Service Runtime package documentation at [http://dl.windowsazure.com/javadoc][azure_javadoc].</span></span>
* <span data-ttu-id="5133b-150">Hallo makecall.jsp code wordt een Twilio-voorwaarde-URL, toegewezen [http://twimlets.com/message][twimlet_message_url], toohello **Url** variabele.</span><span class="sxs-lookup"><span data-stu-id="5133b-150">hello makecall.jsp code assigns a Twilio-provided URL, [http://twimlets.com/message][twimlet_message_url], toohello **Url** variable.</span></span> <span data-ttu-id="5133b-151">Deze URL biedt een Twilio Markup Language (TwiML) antwoord dat informeert Twilio hoe tooproceed Hello aanroepen.</span><span class="sxs-lookup"><span data-stu-id="5133b-151">This URL provides a Twilio Markup Language (TwiML) response that informs Twilio how tooproceed with hello call.</span></span> <span data-ttu-id="5133b-152">Bijvoorbeeld, Hallo TwiML die wordt geretourneerd kunt bevatten een  **&lt;zeg&gt;**  term die resulteert in de tekst wordt gesproken toohello aanroep ontvanger.</span><span class="sxs-lookup"><span data-stu-id="5133b-152">For example, hello TwiML that is returned can contain a **&lt;Say&gt;** verb that results in text being spoken toohello call recipient.</span></span> <span data-ttu-id="5133b-153">In plaats van Hallo geleverde Twilio-URL, kan u uw eigen service toorespond tooTwilio aanvraag; samenstellen Zie voor meer informatie [hoe tooUse Twilio voor spraak- en SMS-mogelijkheden in Java][howto_twilio_voice_sms_java].</span><span class="sxs-lookup"><span data-stu-id="5133b-153">Instead of using hello Twilio-provided URL, you could build your own service toorespond tooTwilio's request; for more information, see [How tooUse Twilio for Voice and SMS Capabilities in Java][howto_twilio_voice_sms_java].</span></span> <span data-ttu-id="5133b-154">Meer informatie over TwiML kan worden gevonden op [http://www.twilio.com/docs/api/twiml][twiml], en meer informatie over  **&lt;zeg&gt;**  en andere Twilio-termen kunnen worden gevonden op [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="5133b-154">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml], and more information about **&lt;Say&gt;** and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>
* <span data-ttu-id="5133b-155">Hallo Twilio-richtlijnen voor beveiliging op lezen [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="5133b-155">Read hello Twilio security guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>

<span data-ttu-id="5133b-156">Zie voor meer informatie over Twilio [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="5133b-156">For additional information about Twilio, see [https://www.twilio.com/docs][twilio_docs].</span></span>

## <a name="see-also"></a><span data-ttu-id="5133b-157">Zie ook</span><span class="sxs-lookup"><span data-stu-id="5133b-157">See Also</span></span>
* <span data-ttu-id="5133b-158">[Hoe tooUse Twilio voor spraak- en SMS-mogelijkheden in Java][howto_twilio_voice_sms_java]</span><span class="sxs-lookup"><span data-stu-id="5133b-158">[How tooUse Twilio for Voice and SMS Capabilities in Java][howto_twilio_voice_sms_java]</span></span>
* <span data-ttu-id="5133b-159">[Toevoegen van een certificaat toohello Java CA-certificaatarchief][add_ca_cert]</span><span class="sxs-lookup"><span data-stu-id="5133b-159">[Adding a Certificate toohello Java CA Certificate Store][add_ca_cert]</span></span>

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
