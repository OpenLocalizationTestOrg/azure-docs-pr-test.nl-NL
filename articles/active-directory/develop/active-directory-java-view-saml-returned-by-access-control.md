---
title: Weergave SAML geretourneerd door de Access Control-Service (Java)
description: Informatie over het weergeven van SAML geretourneerd door de Access Control-Service in Java-toepassingen die worden gehost op Azure.
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
ms.openlocfilehash: 1552e624a4703138ab82f7133ceaec3dbd04e1db
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-view-saml-returned-by-the-azure-access-control-service"></a><span data-ttu-id="1e205-103">SAML geretourneerd door de Azure Access Control-Service weergeven</span><span class="sxs-lookup"><span data-stu-id="1e205-103">How to view SAML returned by the Azure Access Control Service</span></span>
<span data-ttu-id="1e205-104">Deze handleiding wordt beschreven hoe u om weer te geven van de onderliggende Security Assertion Markup Language (SAML) die aan uw toepassing wordt geretourneerd door de Azure Access Control Service (ACS).</span><span class="sxs-lookup"><span data-stu-id="1e205-104">This guide will show you how to view the underlying Security Assertion Markup Language (SAML) returned to your application by the Azure Access Control Service (ACS).</span></span> <span data-ttu-id="1e205-105">De handleiding is gebaseerd op de [Web gebruikers verifiëren met Azure Access Control-Service met behulp van Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) onderwerp, doordat de code die de SAML-informatie weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1e205-105">The guide builds on the [How to Authenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) topic, by providing code that displays the SAML information.</span></span> <span data-ttu-id="1e205-106">De voltooide toepassing ziet er ongeveer als volgt.</span><span class="sxs-lookup"><span data-stu-id="1e205-106">The completed application will look similar to the following.</span></span>

![Voorbeeld van SAML uitvoer][saml_output]

<span data-ttu-id="1e205-108">Zie voor meer informatie over ACS de [Vervolgstappen](#next_steps) sectie.</span><span class="sxs-lookup"><span data-stu-id="1e205-108">For more information on ACS, see the [Next steps](#next_steps) section.</span></span>

> [!NOTE]
> <span data-ttu-id="1e205-109">Het Azure Access Services besturingselement Filter is een community technology preview.</span><span class="sxs-lookup"><span data-stu-id="1e205-109">The Azure Access Services Control Filter is a community technology preview.</span></span> <span data-ttu-id="1e205-110">Als de bètasoftware, wordt deze niet formeel ondersteund door Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1e205-110">As pre-release software, it is not formally supported by Microsoft.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="1e205-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1e205-111">Prerequisites</span></span>
<span data-ttu-id="1e205-112">Voltooi de steekproef op voor het voltooien van de taken in deze handleiding [Web gebruikers verifiëren met Azure Access Control-Service met behulp van Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) en deze gebruiken als startpunt voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="1e205-112">To complete the tasks in this guide, complete the sample at [How to Authenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) and use it as the starting point for this tutorial.</span></span>

## <a name="add-the-jspwriter-library-to-your-build-path-and-deployment-assembly"></a><span data-ttu-id="1e205-113">De bibliotheek JspWriter toevoegen aan uw build-pad en de implementatie-assembly</span><span class="sxs-lookup"><span data-stu-id="1e205-113">Add the JspWriter library to your build path and deployment assembly</span></span>
<span data-ttu-id="1e205-114">Toevoegen van de bibliotheek waarin de **javax.servlet.jsp.JspWriter** klasse naar uw build-pad en de implementatie-assembly.</span><span class="sxs-lookup"><span data-stu-id="1e205-114">Add the library that contains the **javax.servlet.jsp.JspWriter** class to your build path and deployment assembly.</span></span> <span data-ttu-id="1e205-115">Als u Tomcat gebruikt, de bibliotheek is **jsp-api.jar**, die zich bevindt in de Apache **lib** map.</span><span class="sxs-lookup"><span data-stu-id="1e205-115">If you are using Tomcat, the library is **jsp-api.jar**, which is located in the Apache **lib** folder.</span></span>

1. <span data-ttu-id="1e205-116">In de Projectverkenner van Eclipse met de rechtermuisknop op **MyACSHelloWorld**, klikt u op **pad**, klikt u op **configureren pad**, klikt u op de **bibliotheken**tabblad en klik vervolgens op **externe JARs toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="1e205-116">In Eclipse's Project Explorer, right-click **MyACSHelloWorld**, click **Build Path**, click **Configure Build Path**, click the **Libraries** tab, and then click **Add External JARs**.</span></span>
2. <span data-ttu-id="1e205-117">In de **JAR selectie** dialoogvenster, gaat u naar het JAR nodig, selecteert u deze en klik op **Open**.</span><span class="sxs-lookup"><span data-stu-id="1e205-117">In the **JAR Selection** dialog, navigate to the necessary JAR, select it, and then click **Open**.</span></span>
3. <span data-ttu-id="1e205-118">Met de **eigenschappen voor MyACSHelloWorld** dialoogvenster nog geopend, klikt u op **implementatie Assembly**.</span><span class="sxs-lookup"><span data-stu-id="1e205-118">With the **Properties for MyACSHelloWorld** dialog still open, click **Deployment Assembly**.</span></span>
4. <span data-ttu-id="1e205-119">In de **Web Deployment Assembly** dialoogvenster, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="1e205-119">In the **Web Deployment Assembly** dialog, click **Add**.</span></span>
5. <span data-ttu-id="1e205-120">In de **nieuwe Assembly richtlijn** dialoogvenster, klikt u op **Java Build Path vermeldingen** en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="1e205-120">In the **New Assembly Directive** dialog, click **Java Build Path Entries** and then click **Next**.</span></span>
6. <span data-ttu-id="1e205-121">Selecteer de juiste bibliotheek en klik op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="1e205-121">Select the appropriate library and click **Finish**.</span></span>
7. <span data-ttu-id="1e205-122">Klik op **OK** sluiten de **eigenschappen voor MyACSHelloWorld** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1e205-122">Click **OK** to close the **Properties for MyACSHelloWorld** dialog.</span></span>

## <a name="modify-the-jsp-file-to-display-saml"></a><span data-ttu-id="1e205-123">Wijzigen van het JSP-bestand om SAML weer te geven</span><span class="sxs-lookup"><span data-stu-id="1e205-123">Modify the JSP file to display SAML</span></span>
<span data-ttu-id="1e205-124">Wijzig **index.jsp** gebruiken de volgende code.</span><span class="sxs-lookup"><span data-stu-id="1e205-124">Modify **index.jsp** to use the following code.</span></span>

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

                                 // If it is a text node, just print the text.
                                 if (list.item(0).getNodeName() == "#text")
                                 {
                                     out.println("Text value: <b>" + list.item(0).getTextContent() + "</b><br>");
                                 }
                                 else
                                 {
                                     // Print out the child node names.
                                     out.print("Contains " + nChild + " child node(s): ");   
                                        for (i=0; i < nChild; i++)
                                     {
                                        Node temp = list.item(i);

                                        out.print("<b>" + temp.getNodeName() + "</b>");
                                        if (i < nChild - 1)
                                        {
                                            // Separate the names.
                                            out.print(", ");
                                        }
                                        else
                                        {
                                            // Finish the sentence.
                                            out.print(".");
                                        }

                                     }
                                     out.println("<br>");

                                     // Process the child nodes.
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

            // Iterate the child nodes of the doc.
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

## <a name="run-the-application"></a><span data-ttu-id="1e205-125">De toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="1e205-125">Run the application</span></span>
1. <span data-ttu-id="1e205-126">Voer uw toepassing in de emulator van de computer of implementeren naar Azure met behulp van de stappen beschreven op [Web gebruikers verifiëren met Azure Access Control-Service met behulp van Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="1e205-126">Run your application in the computer emulator or deploy to Azure, using the steps documented at [How to Authenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md).</span></span>
2. <span data-ttu-id="1e205-127">Een browser starten en open uw webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="1e205-127">Launch a browser and open your web application.</span></span> <span data-ttu-id="1e205-128">Nadat u zich bij uw toepassing aanmelden, ziet u de SAML-informatie, waaronder de security assertion geleverd door de identiteitsprovider.</span><span class="sxs-lookup"><span data-stu-id="1e205-128">After you log on to your application, you'll see SAML information, including the security assertion provided by the identity provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e205-129">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1e205-129">Next steps</span></span>
<span data-ttu-id="1e205-130">Verder verkennen van ACS-functionaliteit en om te experimenteren met meer geavanceerde scenario's, Zie [Access Control Service 2.0][Access Control Service 2.0].</span><span class="sxs-lookup"><span data-stu-id="1e205-130">To further explore ACS's functionality and to experiment with more sophisticated scenarios, see [Access Control Service 2.0][Access Control Service 2.0].</span></span>

[Prerequisites]: #pre
[Modify the JSP file to display SAML]: #modify_jsp
[Add the JspWriter library to your build path and deployment assembly]: #add_library
[Run the application]: #run_application
[Next steps]: #next_steps
[Access Control Service 2.0]: http://go.microsoft.com/fwlink/?LinkID=212360
[How to Authenticate Web Users with Azure Access Control Service Using Eclipse]: active-directory-java-authenticate-users-access-control-eclipse
[saml_output]: ./media/active-directory-java-view-saml-returned-by-access-control/SAML_Output.png
