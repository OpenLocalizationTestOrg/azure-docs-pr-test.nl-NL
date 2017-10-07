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
# <a name="how-tooview-saml-returned-by-hello-azure-access-control-service"></a>Hoe tooview SAML geretourneerd door hello Azure Access Control Service
Deze handleiding leert u hoe tooview Hallo onderliggende Security Assertion Markup Language (SAML) tooyour toepassing geretourneerd door hello Azure Access Control Service (ACS). Hallo handleiding bouwt voort op Hallo [hoe tooAuthenticate webgebruikers met Azure Access Control-Service met behulp van Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) onderwerp, doordat de code die wordt Hallo SAML informatie weergegeven. toepassing Hello voltooid, ziet er vergelijkbare toohello volgende.

![Voorbeeld van SAML uitvoer][saml_output]

Zie voor meer informatie over ACS Hallo [Vervolgstappen](#next_steps) sectie.

> [!NOTE]
> Hello Azure Access Control servicefilter is een community technology preview. Als de bètasoftware, wordt deze niet formeel ondersteund door Microsoft.
> 
> 

## <a name="prerequisites"></a>Vereisten
toocomplete hello taken in deze handleiding, volledige voorbeeld op Hallo [hoe tooAuthenticate webgebruikers met Azure Access Control-Service met behulp van Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) en deze als startpunt voor deze zelfstudie hello gebruiken.

## <a name="add-hello-jspwriter-library-tooyour-build-path-and-deployment-assembly"></a>Hallo JspWriter bibliotheek tooyour build pad en de implementatie-assembly toevoegen
Hallo-bibliotheek met Hallo toevoegen **javax.servlet.jsp.JspWriter** tooyour klasse bouwen assembly-pad en de implementatie. Als u Tomcat Hallo-bibliotheek is **jsp-api.jar**, die zich bevindt in Hallo Apache **lib** map.

1. In de Projectverkenner van Eclipse met de rechtermuisknop op **MyACSHelloWorld**, klikt u op **pad**, klikt u op **-pad configureren**, klikt u op Hallo **bibliotheken** tabblad en klik vervolgens op **externe JARs toevoegen**.
2. In Hallo **JAR selectie** dialoogvenster navigeren toohello nodig JAR selecteren en klik vervolgens op **Open**.
3. Hello **eigenschappen voor MyACSHelloWorld** dialoogvenster nog geopend, klikt u op **implementatie Assembly**.
4. In Hallo **Web Deployment Assembly** dialoogvenster, klikt u op **toevoegen**.
5. In Hallo **nieuwe Assembly richtlijn** dialoogvenster, klikt u op **Java Build Path vermeldingen** en klik vervolgens op **volgende**.
6. Selecteer de juiste bibliotheek Hallo en klik op **voltooien**.
7. Klik op **OK** tooclose hello **eigenschappen voor MyACSHelloWorld** dialoogvenster.

## <a name="modify-hello-jsp-file-toodisplay-saml"></a>Hallo JSP-bestand toodisplay SAML wijzigen
Wijzig **index.jsp** toouse Hallo code te volgen.

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

## <a name="run-hello-application"></a>Hallo-toepassing uitvoeren
1. Uw toepassing uitvoeren in Hallo computer emulator of implementeren van tooAzure, met behulp van Hallo stappen beschreven op [hoe tooAuthenticate webgebruikers met Azure Access Control-Service met behulp van Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md).
2. Een browser starten en open uw webtoepassing. Nadat u tooyour toepassing hebt aangemeld, ziet u de SAML-informatie, waaronder Hallo security assertion geleverd door de identiteitsprovider Hallo.

## <a name="next-steps"></a>Volgende stappen
toofurther verkennen van ACS-functionaliteit en tooexperiment met meer geavanceerde scenario's, Zie [Access Control Service 2.0][Access Control Service 2.0].

[Prerequisites]: #pre
[Modify hello JSP file toodisplay SAML]: #modify_jsp
[Add hello JspWriter library tooyour build path and deployment assembly]: #add_library
[Run hello application]: #run_application
[Next steps]: #next_steps
[Access Control Service 2.0]: http://go.microsoft.com/fwlink/?LinkID=212360
[How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse]: active-directory-java-authenticate-users-access-control-eclipse
[saml_output]: ./media/active-directory-java-view-saml-returned-by-access-control/SAML_Output.png
