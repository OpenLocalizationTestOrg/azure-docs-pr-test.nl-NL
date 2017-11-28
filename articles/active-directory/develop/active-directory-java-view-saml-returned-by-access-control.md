---
title: aaaView SAML geretourneerd door Hallo Access Control Service (Java)
description: Meer informatie over hoe tooview SAML geretourneerd door Hallo Access Control-Service in Java-toepassingen worden gehost op Azure.
services: active-directory
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 6cd216f9-eb43-46b4-b30d-f194d0ae2d48
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.custom: aaddev
ms.openlocfilehash: b6733bc98b505cfa89a4ce456f368ee15da11427
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooview-saml-returned-by-hello-azure-access-control-service"></a><span data-ttu-id="016cf-103">Hoe tooview SAML geretourneerd door hello Azure Access Control Service</span><span class="sxs-lookup"><span data-stu-id="016cf-103">How tooview SAML returned by hello Azure Access Control Service</span></span>
<span data-ttu-id="016cf-104">Deze handleiding leert u hoe tooview Hallo onderliggende Security Assertion Markup Language (SAML) tooyour toepassing geretourneerd door hello Azure Access Control Service (ACS).</span><span class="sxs-lookup"><span data-stu-id="016cf-104">This guide will show you how tooview hello underlying Security Assertion Markup Language (SAML) returned tooyour application by hello Azure Access Control Service (ACS).</span></span> <span data-ttu-id="016cf-105">Hallo handleiding bouwt voort op Hallo [hoe tooAuthenticate webgebruikers met Azure Access Control-Service met behulp van Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) onderwerp, doordat de code die wordt Hallo SAML informatie weergegeven.</span><span class="sxs-lookup"><span data-stu-id="016cf-105">hello guide builds on hello [How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) topic, by providing code that displays hello SAML information.</span></span> <span data-ttu-id="016cf-106">toepassing Hello voltooid, ziet er vergelijkbare toohello volgende.</span><span class="sxs-lookup"><span data-stu-id="016cf-106">hello completed application will look similar toohello following.</span></span>

![Voorbeeld van SAML uitvoer][saml_output]

<span data-ttu-id="016cf-108">Zie voor meer informatie over ACS Hallo [Vervolgstappen](#next_steps) sectie.</span><span class="sxs-lookup"><span data-stu-id="016cf-108">For more information on ACS, see hello [Next steps](#next_steps) section.</span></span>

> [!NOTE]
> <span data-ttu-id="016cf-109">Hello Azure Access Control servicefilter is een community technology preview.</span><span class="sxs-lookup"><span data-stu-id="016cf-109">hello Azure Access Services Control Filter is a community technology preview.</span></span> <span data-ttu-id="016cf-110">Als de bètasoftware, wordt deze niet formeel ondersteund door Microsoft.</span><span class="sxs-lookup"><span data-stu-id="016cf-110">As pre-release software, it is not formally supported by Microsoft.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="016cf-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="016cf-111">Prerequisites</span></span>
<span data-ttu-id="016cf-112">toocomplete hello taken in deze handleiding, volledige voorbeeld op Hallo [hoe tooAuthenticate webgebruikers met Azure Access Control-Service met behulp van Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) en deze als startpunt voor deze zelfstudie hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="016cf-112">toocomplete hello tasks in this guide, complete hello sample at [How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) and use it as hello starting point for this tutorial.</span></span>

## <a name="add-hello-jspwriter-library-tooyour-build-path-and-deployment-assembly"></a><span data-ttu-id="016cf-113">Hallo JspWriter bibliotheek tooyour build pad en de implementatie-assembly toevoegen</span><span class="sxs-lookup"><span data-stu-id="016cf-113">Add hello JspWriter library tooyour build path and deployment assembly</span></span>
<span data-ttu-id="016cf-114">Hallo-bibliotheek met Hallo toevoegen **javax.servlet.jsp.JspWriter** tooyour klasse bouwen assembly-pad en de implementatie.</span><span class="sxs-lookup"><span data-stu-id="016cf-114">Add hello library that contains hello **javax.servlet.jsp.JspWriter** class tooyour build path and deployment assembly.</span></span> <span data-ttu-id="016cf-115">Als u Tomcat Hallo-bibliotheek is **jsp-api.jar**, die zich bevindt in Hallo Apache **lib** map.</span><span class="sxs-lookup"><span data-stu-id="016cf-115">If you are using Tomcat, hello library is **jsp-api.jar**, which is located in hello Apache **lib** folder.</span></span>

1. <span data-ttu-id="016cf-116">In de Projectverkenner van Eclipse met de rechtermuisknop op **MyACSHelloWorld**, klikt u op **pad**, klikt u op **-pad configureren**, klikt u op Hallo **bibliotheken** tabblad en klik vervolgens op **externe JARs toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="016cf-116">In Eclipse's Project Explorer, right-click **MyACSHelloWorld**, click **Build Path**, click **Configure Build Path**, click hello **Libraries** tab, and then click **Add External JARs**.</span></span>
2. <span data-ttu-id="016cf-117">In Hallo **JAR selectie** dialoogvenster navigeren toohello nodig JAR selecteren en klik vervolgens op **Open**.</span><span class="sxs-lookup"><span data-stu-id="016cf-117">In hello **JAR Selection** dialog, navigate toohello necessary JAR, select it, and then click **Open**.</span></span>
3. <span data-ttu-id="016cf-118">Hello **eigenschappen voor MyACSHelloWorld** dialoogvenster nog geopend, klikt u op **implementatie Assembly**.</span><span class="sxs-lookup"><span data-stu-id="016cf-118">With hello **Properties for MyACSHelloWorld** dialog still open, click **Deployment Assembly**.</span></span>
4. <span data-ttu-id="016cf-119">In Hallo **Web Deployment Assembly** dialoogvenster, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="016cf-119">In hello **Web Deployment Assembly** dialog, click **Add**.</span></span>
5. <span data-ttu-id="016cf-120">In Hallo **nieuwe Assembly richtlijn** dialoogvenster, klikt u op **Java Build Path vermeldingen** en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="016cf-120">In hello **New Assembly Directive** dialog, click **Java Build Path Entries** and then click **Next**.</span></span>
6. <span data-ttu-id="016cf-121">Selecteer de juiste bibliotheek Hallo en klik op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="016cf-121">Select hello appropriate library and click **Finish**.</span></span>
7. <span data-ttu-id="016cf-122">Klik op **OK** tooclose hello **eigenschappen voor MyACSHelloWorld** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="016cf-122">Click **OK** tooclose hello **Properties for MyACSHelloWorld** dialog.</span></span>

## <a name="modify-hello-jsp-file-toodisplay-saml"></a><span data-ttu-id="016cf-123">Hallo JSP-bestand toodisplay SAML wijzigen</span><span class="sxs-lookup"><span data-stu-id="016cf-123">Modify hello JSP file toodisplay SAML</span></span>
<span data-ttu-id="016cf-124">Wijzig **index.jsp** toouse Hallo code te volgen.</span><span class="sxs-lookup"><span data-stu-id="016cf-124">Modify **index.jsp** toouse hello following code.</span></span>

    <%@ page language="java" contentType="text/html; charset=UTF-8"
        pageEncoding="UTF-8"%>
        <%@ page import="javax.xml.parsers.*"
                 import="javax.xml.transform.*"
                 import="org.w3c.dom.*"
                 import="java.io.*"
                 import="javax.xml.transform.stream.*"
                 import="javax.xml.transform.dom.*"
                 import="javax.xml.xpath.*"
                 import="javax.servlet.jsp.JspWriter" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Sample ACS Filter</title>
    </head>
    <body>
        <h3>SAML information from sample ACS program</h3>
        <%!
        void displaySAMLInfo(Node node, String parent, JspWriter out)
        {

            try
            {
                String nodeName;
                int nChild, i;

                nodeName = node.getNodeName();
                out.println("<br>");
                out.println("<u>Examining <b>" + parent + nodeName + "</b></u><br>");

                   // Attributes.
                   NamedNodeMap attribsMap = node.getAttributes();
                   if (null != attribsMap)
                   {
                         for (i=0; i < attribsMap.getLength(); i++)
                         {
                                Node attrib = attribsMap.item(i);
                                out.println("Attribute: <b>" + attrib.getNodeName() + "</b>: " + attrib.getNodeValue()  + "<br>");
                         }
                   }

                   // Child nodes.
                   NodeList list = node.getChildNodes();
                   if (null != list)
                    {
                          nChild = list.getLength();
                          if (nChild > 0)
                          {                    

                                 // If it is a text node, just print hello text.
                                 if (list.item(0).getNodeName() == "#text")
                                 {
                                     out.println("Text value: <b>" + list.item(0).getTextContent() + "</b><br>");
                                 }
                                 else
                                 {
                                     // Print out hello child node names.
                                     out.print("Contains " + nChild + " child node(s): ");   
                                        for (i=0; i < nChild; i++)
                                     {
                                        Node temp = list.item(i);

                                        out.print("<b>" + temp.getNodeName() + "</b>");
                                        if (i < nChild - 1)
                                        {
                                            // Separate hello names.
                                            out.print(", ");
                                        }
                                        else
                                        {
                                            // Finish hello sentence.
                                            out.print(".");
                                        }

                                     }
                                     out.println("<br>");

                                     // Process hello child nodes.
                                     for (i=0; i < nChild; i++)
                                     {
                                        Node temp = list.item(i);
                                        displaySAMLInfo(temp, parent + nodeName + "\\", out);
                                     }
                               }
                          }
                      }
                  }
                catch (Exception e)
                {
                    System.out.println("Exception encountered.");
                    e.printStackTrace();            
                }
            }
        %>

        <%
        try
        {
            String data  = (String) request.getAttribute("ACSSAML");

            DocumentBuilder docBuilder;
            Document doc = null;
            DocumentBuilderFactory docBuilderFactory = DocumentBuilderFactory.newInstance();
            docBuilderFactory.setIgnoringElementContentWhitespace(true);
            docBuilder = docBuilderFactory.newDocumentBuilder();
            byte[] xmlDATA = data.getBytes();

            ByteArrayInputStream in = new ByteArrayInputStream(xmlDATA);
            doc = docBuilder.parse(in);
            doc.getDocumentElement().normalize();

            // Iterate hello child nodes of hello doc.
            NodeList list = doc.getChildNodes();

            for (int i=0; i < list.getLength(); i++)
            {
                displaySAMLInfo(list.item(i), "", out);
            }
        }
        catch (Exception e)
        {
            out.println("Exception encountered.");
            e.printStackTrace();
        }

        %>
    </body>
    </html>

## <a name="run-hello-application"></a><span data-ttu-id="016cf-125">Hallo-toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="016cf-125">Run hello application</span></span>
1. <span data-ttu-id="016cf-126">Uw toepassing uitvoeren in Hallo computer emulator of implementeren van tooAzure, met behulp van Hallo stappen beschreven op [hoe tooAuthenticate webgebruikers met Azure Access Control-Service met behulp van Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="016cf-126">Run your application in hello computer emulator or deploy tooAzure, using hello steps documented at [How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md).</span></span>
2. <span data-ttu-id="016cf-127">Een browser starten en open uw webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="016cf-127">Launch a browser and open your web application.</span></span> <span data-ttu-id="016cf-128">Nadat u tooyour toepassing hebt aangemeld, ziet u de SAML-informatie, waaronder Hallo security assertion geleverd door de identiteitsprovider Hallo.</span><span class="sxs-lookup"><span data-stu-id="016cf-128">After you log on tooyour application, you'll see SAML information, including hello security assertion provided by hello identity provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="016cf-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="016cf-129">Next steps</span></span>
<span data-ttu-id="016cf-130">toofurther verkennen van ACS-functionaliteit en tooexperiment met meer geavanceerde scenario's, Zie [Access Control Service 2.0][Access Control Service 2.0].</span><span class="sxs-lookup"><span data-stu-id="016cf-130">toofurther explore ACS's functionality and tooexperiment with more sophisticated scenarios, see [Access Control Service 2.0][Access Control Service 2.0].</span></span>

[Prerequisites]: #pre
[Modify hello JSP file toodisplay SAML]: #modify_jsp
[Add hello JspWriter library tooyour build path and deployment assembly]: #add_library
[Run hello application]: #run_application
[Next steps]: #next_steps
[Access Control Service 2.0]: http://go.microsoft.com/fwlink/?LinkID=212360
[How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse]: active-directory-java-authenticate-users-access-control-eclipse
[saml_output]: ./media/active-directory-java-view-saml-returned-by-access-control/SAML_Output.png
