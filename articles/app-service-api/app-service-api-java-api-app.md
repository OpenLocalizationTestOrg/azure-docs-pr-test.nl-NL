---
title: aaaBuild en implementeren van een Java API-app in Azure App Service
description: Meer informatie over hoe een Java API-app toocreate verpakken en distribueren van tooAzure App Service.
services: app-service\api
documentationcenter: java
author: rmcmurray
manager: erikre
editor: tdykstra
ms.assetid: 8d21ba5f-fc57-4269-bc8f-2fcab936ec22
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: get-started-article
ms.date: 04/25/2017
ms.author: rachelap;robmcm
ms.openlocfilehash: a4056fec870b1c4bed8ee14bb0e748b3ee89b9e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-a-java-api-app-in-azure-app-service"></a><span data-ttu-id="5a58c-103">Een Java API-app bouwen en implementeren in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="5a58c-103">Build and deploy a Java API app in Azure App Service</span></span>
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="5a58c-104">Deze zelfstudie laat zien hoe toocreate een Java-toepassing en implementeer deze tooAzure App Service API-Apps met behulp van [Git].</span><span class="sxs-lookup"><span data-stu-id="5a58c-104">This tutorial shows how toocreate a Java application and deploy it tooAzure App Service API Apps using [Git].</span></span> <span data-ttu-id="5a58c-105">Hallo-instructies in deze zelfstudie kunnen worden uitgevoerd op elk besturingssysteem waarmee Java uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5a58c-105">hello instructions in this tutorial can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="5a58c-106">Hallo-code in deze zelfstudie wordt gebouwd met [Maven].</span><span class="sxs-lookup"><span data-stu-id="5a58c-106">hello code in this tutorial is built using [Maven].</span></span> <span data-ttu-id="5a58c-107">[Jax-RS] gebruikte toocreate hello RESTful-Service is en is gegenereerd op basis van Hallo [Swagger] metagegevens specificatie Hallo met [Swagger Editor].</span><span class="sxs-lookup"><span data-stu-id="5a58c-107">[Jax-RS] is used toocreate hello RESTful Service, and is generated based on hello [Swagger] metadata specification using hello [Swagger Editor].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a58c-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="5a58c-108">Prerequisites</span></span>
1. <span data-ttu-id="5a58c-109">[Java Development Kit 8] \(of hoger)</span><span class="sxs-lookup"><span data-stu-id="5a58c-109">[Java Developer's Kit 8] \(or later)</span></span>
2. <span data-ttu-id="5a58c-110">[Maven] is geïnstalleerd op uw ontwikkelcomputer</span><span class="sxs-lookup"><span data-stu-id="5a58c-110">[Maven] installed on your development machine</span></span>
3. <span data-ttu-id="5a58c-111">[Git] is geïnstalleerd op uw ontwikkelcomputer</span><span class="sxs-lookup"><span data-stu-id="5a58c-111">[Git] installed on your development machine</span></span>
4. <span data-ttu-id="5a58c-112">Een betaald of [gratis proefversie] abonnement te[Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="5a58c-112">A paid or [free trial] subscription too[Microsoft Azure]</span></span>
5. <span data-ttu-id="5a58c-113">Een HTTP-testtoepassing zoals [Postman]</span><span class="sxs-lookup"><span data-stu-id="5a58c-113">An HTTP test application like [Postman]</span></span>

## <a name="scaffold-hello-api-using-swaggerio"></a><span data-ttu-id="5a58c-114">Scaffold hello API met behulp van Swagger.IO</span><span class="sxs-lookup"><span data-stu-id="5a58c-114">Scaffold hello API using Swagger.IO</span></span>
<span data-ttu-id="5a58c-115">Hallo online-editor swagger.io kunt u Swagger JSON- of YAML-code die Hallo-structuur van uw API vertegenwoordigt invoeren.</span><span class="sxs-lookup"><span data-stu-id="5a58c-115">Using hello swagger.io online editor, you can enter Swagger JSON or YAML code representing hello structure of your API.</span></span> <span data-ttu-id="5a58c-116">Zodra u Hallo API oppervlak ontworpen hebt, kunt u code voor verschillende platforms en frameworks exporteren.</span><span class="sxs-lookup"><span data-stu-id="5a58c-116">Once you have hello API surface area designed, you can export code for a variety of platforms and frameworks.</span></span> <span data-ttu-id="5a58c-117">In de volgende sectie hello, Hallo die code gewijzigde tooinclude mock-functionaliteit niet.</span><span class="sxs-lookup"><span data-stu-id="5a58c-117">In hello next section, hello scaffolded code will be modified tooinclude mock functionality.</span></span> 

<span data-ttu-id="5a58c-118">Deze demonstratie begint met een Swagger JSON-hoofdtekst die u in de editor swagger.io hello, wordt plakken die wordt vervolgens worden gebruikte toogenerate code waarbij gebruik wordt gemaakt van JAX-RS tooaccess een REST-API-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="5a58c-118">This demonstration will begin with a Swagger JSON body that you will paste into hello swagger.io editor, which will then be used toogenerate code making use of JAX-RS tooaccess a REST API endpoint.</span></span> <span data-ttu-id="5a58c-119">Vervolgens bewerkt u Hallo die code tooreturn Hiermee mock-gegevens, een REST-API die is gebouwd op een mechanisme simuleren.</span><span class="sxs-lookup"><span data-stu-id="5a58c-119">Then, you'll edit hello scaffolded code tooreturn mock data, simulating a REST API built atop a data persistence mechanism.</span></span>  

1. <span data-ttu-id="5a58c-120">Hallo volgende Swagger JSON-code tooyour Klembord kopiëren:</span><span class="sxs-lookup"><span data-stu-id="5a58c-120">Copy hello following Swagger JSON code tooyour clipboard:</span></span>
   
        {
            "swagger": "2.0",
            "info": {
                "version": "v1",
                "title": "Contact List",
                "description": "A Contact list API based on Swagger and built using Java"
            },
            "host": "localhost",
            "schemes": [
                "http",
                "https"
            ],
            "basePath": "/api",
            "paths": {
                "/contacts": {
                    "get": {
                        "tags": [
                            "Contact"
                        ],
                        "operationId": "contacts_get",
                        "consumes": [],
                        "produces": [
                            "application/json",
                            "text/json"
                        ],
                        "responses": {
                            "200": {
                                "description": "OK",
                                "schema": {
                                    "type": "array",
                                    "items": {
                                        "$ref": "#/definitions/Contact"
                                    }
                                }
                            }
                        },
                        "deprecated": false
                    }
                },
                "/contacts/{id}": {
                    "get": {
                        "tags": [
                            "Contact"
                        ],
                        "operationId": "contacts_getById",
                        "consumes": [],
                        "produces": [
                            "application/json",
                            "text/json"
                        ],
                        "parameters": [
                            {
                                "name": "id",
                                "in": "path",
                                "required": true,
                                "type": "integer",
                                "format": "int32"
                            }
                        ],
                        "responses": {
                            "200": {
                                "description": "OK",
                                "schema": {
                                    "type": "array",
                                    "items": {
                                        "$ref": "#/definitions/Contact"
                                    }
                                }
                            }
                        },
                        "deprecated": false
                    }
                }
            },
            "definitions": {
                "Contact": {
                    "type": "object",
                    "properties": {
                        "Id": {
                            "format": "int32",
                            "type": "integer"
                        },
                        "Name": {
                            "type": "string"
                        },
                        "EmailAddress": {
                            "type": "string"
                        }
                    }
                }
            }
        }
2. <span data-ttu-id="5a58c-121">Navigeer toohello [Online Swagger Editor].</span><span class="sxs-lookup"><span data-stu-id="5a58c-121">Navigate toohello [Online Swagger Editor].</span></span> <span data-ttu-id="5a58c-122">Klik Hallo **File -> Paste JSON** menu-item.</span><span class="sxs-lookup"><span data-stu-id="5a58c-122">Once there, click hello **File -> Paste JSON** menu item.</span></span>
   
    ![Menuopdracht Paste JSON][paste-json]
3. <span data-ttu-id="5a58c-124">Plak in Hallo contactpersonen lijst API Swagger JSON u eerder hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="5a58c-124">Paste in hello Contacts List API Swagger JSON you copied earlier.</span></span> 
   
    ![JSON-code plakken in Swagger][pasted-swagger]
4. <span data-ttu-id="5a58c-126">Hallo-documentatie pagina's en API-overzicht weergegeven in het Hallo-editor weergeven.</span><span class="sxs-lookup"><span data-stu-id="5a58c-126">View hello documentation pages and API summary rendered in hello editor.</span></span> 
   
    ![Door Swagger gegenereerde documenten weergeven][view-swagger-generated-docs]
5. <span data-ttu-id="5a58c-128">Selecteer Hallo **Generate Server -> JAX-RS** menu optie tooscaffold Hallo servercode u later tooadd mock-implementatie gaat bewerken.</span><span class="sxs-lookup"><span data-stu-id="5a58c-128">Select hello **Generate Server -> JAX-RS** menu option tooscaffold hello server-side code you'll edit later tooadd mock implementation.</span></span> 
   
    ![Menuopdracht Generate Code][generate-code-menu-item]
   
    <span data-ttu-id="5a58c-130">Zodra het Hallo-code is gegenereerd, is het hebt dat u een ZIP-bestand toodownload worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="5a58c-130">Once hello code is generated, you'll be provided a ZIP file toodownload.</span></span> <span data-ttu-id="5a58c-131">Dit bestand bevat Hallo-code die door de Swagger-codegenerator Hallo en alle gekoppelde bouwscripts.</span><span class="sxs-lookup"><span data-stu-id="5a58c-131">This file contains hello code scaffolded by hello Swagger code generator and all associated build scripts.</span></span> <span data-ttu-id="5a58c-132">Pak Hallo hele bibliotheek tooa map op uw ontwikkelwerkstation.</span><span class="sxs-lookup"><span data-stu-id="5a58c-132">Unzip hello entire library tooa directory on your development workstation.</span></span> 

## <a name="edit-hello-code-tooadd-api-implementation"></a><span data-ttu-id="5a58c-133">Hallo Code tooadd API implementatie bewerken</span><span class="sxs-lookup"><span data-stu-id="5a58c-133">Edit hello Code tooadd API Implementation</span></span>
<span data-ttu-id="5a58c-134">In deze sectie zult u Hallo Swagger gegenereerde code serverimplementatie vervangen door uw eigen aangepaste code.</span><span class="sxs-lookup"><span data-stu-id="5a58c-134">In this section, you'll replace hello Swagger-generated code's server-side implementation with your custom code.</span></span> <span data-ttu-id="5a58c-135">Hallo nieuwe code wordt een Matrixlijst met entiteiten toohello aanroepende client geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="5a58c-135">hello new code will return an ArrayList of Contact entities toohello calling client.</span></span> 

1. <span data-ttu-id="5a58c-136">Open Hallo *Contact.java* modelbestand dat in Hallo bevindt zich *src/gen/java/io/swagger/model* map met [Visual Studio Code] of uw favoriete teksteditor.</span><span class="sxs-lookup"><span data-stu-id="5a58c-136">Open hello *Contact.java* model file, which is located in hello *src/gen/java/io/swagger/model* folder, using [Visual Studio Code] or your favorite text editor.</span></span> 
   
    ![Modelbestand voor contactpersonen openen][open-contact-model-file]
2. <span data-ttu-id="5a58c-138">Toevoegen van de volgende constructor binnen Hallo Hallo **Contact** klasse.</span><span class="sxs-lookup"><span data-stu-id="5a58c-138">Add hello following constructor within hello **Contact** class.</span></span> 
   
        public Contact(Integer id, String name, String email) 
        {
            this.id = id;
            this.name = name;
            this.emailAddress = email;
        }
3. <span data-ttu-id="5a58c-139">Open Hallo *ContactsApiServiceImpl.java* service-implementatiebestand dat in Hallo bevindt zich *src/main/java/io/swagger/api/impl* map met [Visual Studio Code]of uw favoriete teksteditor.</span><span class="sxs-lookup"><span data-stu-id="5a58c-139">Open hello *ContactsApiServiceImpl.java* service implementation file, which is located in hello *src/main/java/io/swagger/api/impl* folder, using [Visual Studio Code] or your favorite text editor.</span></span>
   
    ![Servicecodebestand voor contactpersonen openen][open-contact-service-code-file]
4. <span data-ttu-id="5a58c-141">Hallo-code in Hallo bestand overschrijven met deze nieuwe code tooadd een code toohello mock-implementatie.</span><span class="sxs-lookup"><span data-stu-id="5a58c-141">Overwrite hello code in hello file with this new code tooadd a mock implementation toohello service code.</span></span> 
   
        package io.swagger.api.impl;
   
        import io.swagger.api.*;
        
        import io.swagger.model.Contact;
        import java.util.*;
        import io.swagger.api.NotFoundException;
               
        import javax.ws.rs.core.Response;
        import javax.ws.rs.core.SecurityContext;
   
        @javax.annotation.Generated(value = "class io.swagger.codegen.languages.JaxRSServerCodegen", date = "2015-11-24T21:54:11.648Z")
        public class ContactsApiServiceImpl extends ContactsApiService {
   
            private ArrayList<Contact> loadContacts()
            {
                ArrayList<Contact> list = new ArrayList<Contact>();
                list.add(new Contact(1, "Barney Poland", "barney@contoso.com"));
                list.add(new Contact(2, "Lacy Barrera", "lacy@contoso.com"));
                list.add(new Contact(3, "Lora Riggs", "lora@contoso.com"));
                return list;
            }
   
            @Override
            public Response contactsGet(SecurityContext securityContext)
            throws NotFoundException {
                ArrayList<Contact> list = loadContacts();
                return Response.ok().entity(list).build();
                }
   
            @Override
            public Response contactsGetById(Integer id, SecurityContext securityContext)
            throws NotFoundException {
                ArrayList<Contact> list = loadContacts();
                Contact ret = null;
   
                for(int i=0; i<list.size(); i++)
                {
                    if(list.get(i).getId() == id)
                        {
                            ret = list.get(i);
                        }
                }
                return Response.ok().entity(ret).build();
            }
        }
5. <span data-ttu-id="5a58c-142">Open een opdrachtprompt en wijzig directory toohello hoofdmap van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="5a58c-142">Open a command prompt and change directory toohello root folder of your application.</span></span>
6. <span data-ttu-id="5a58c-143">Hallo volgende Maven-opdracht toobuild Hallo code uitvoeren en voer dit lokaal met behulp van Hallo Jetty-app-server.</span><span class="sxs-lookup"><span data-stu-id="5a58c-143">Execute hello following Maven command toobuild hello code and run it using hello Jetty app server locally.</span></span> 
   
        mvn package jetty:run
7. <span data-ttu-id="5a58c-144">U ziet Hallo-opdrachtvenster weer dat Jetty uw code via poort 8080 is gestart.</span><span class="sxs-lookup"><span data-stu-id="5a58c-144">You should see hello command window reflect that Jetty has started your code on port 8080.</span></span> 
   
    ![Servicecodebestand voor contactpersonen openen][run-jetty-war]
8. <span data-ttu-id="5a58c-146">Gebruik [Postman] toomake een aanvraag toohello 'ophalen van alle contactpersonen' API-methode via http://localhost: 8080/api/contacts.</span><span class="sxs-lookup"><span data-stu-id="5a58c-146">Use [Postman] toomake a request toohello "get all contacts" API method at http://localhost:8080/api/contacts.</span></span>
   
    ![Hallo API voor contactpersonen aanroepen][calling-contacts-api]
9. <span data-ttu-id="5a58c-148">Gebruik [Postman] toomake een aanvraag toohello 'ophalen van een specifieke contactpersoon' API-methode zich bevindt op http://localhost: 8080/api/contacts/2.</span><span class="sxs-lookup"><span data-stu-id="5a58c-148">Use [Postman] toomake a request toohello "get specific contact" API method located at http://localhost:8080/api/contacts/2.</span></span>
   
    ![Hallo API voor contactpersonen aanroepen][calling-specific-contact-api]
10. <span data-ttu-id="5a58c-150">Bouw ten slotte Hallo Java WAR (webarchief)-bestand door het uitvoeren van Hallo volgende Maven-opdracht in de console.</span><span class="sxs-lookup"><span data-stu-id="5a58c-150">Finally, build hello Java WAR (Web ARchive) file by executing hello following Maven command in your console.</span></span> 
    
         mvn package war:war
11. <span data-ttu-id="5a58c-151">Als Hallo WAR-bestand is gebouwd, wordt deze geplaatst in Hallo **doel** map.</span><span class="sxs-lookup"><span data-stu-id="5a58c-151">Once hello WAR file is built, it will be placed into hello **target** folder.</span></span> <span data-ttu-id="5a58c-152">Navigeer naar Hallo **doel** map en wijzig de naam Hallo u WAR-bestand te**ROOT.war**.</span><span class="sxs-lookup"><span data-stu-id="5a58c-152">Navigate into hello **target** folder and rename hello WAR file too**ROOT.war**.</span></span> <span data-ttu-id="5a58c-153">(Zorg ervoor dat Hallo hoofdlettergebruik overeenkomt met deze indeling).</span><span class="sxs-lookup"><span data-stu-id="5a58c-153">(Make sure hello capitalization matches this format).</span></span>
    
          rename swagger-jaxrs-server-1.0.0.war ROOT.war
12. <span data-ttu-id="5a58c-154">Ten slotte uitvoeren Hallo volgende opdrachten uit Hallo hoofdmap van uw toepassing toocreate een **implementeren** tooAzure map toouse toodeploy Hallo WAR-bestand.</span><span class="sxs-lookup"><span data-stu-id="5a58c-154">Finally, execute hello following commands from hello root folder of your application toocreate a **deploy** folder toouse toodeploy hello WAR file tooAzure.</span></span> 
    
          mkdir deploy
          mkdir deploy\webapps
          copy target\ROOT.war deploy\webapps
          cd deploy

## <a name="publish-hello-output-tooazure-app-service"></a><span data-ttu-id="5a58c-155">Hallo uitvoer tooAzure App Service publiceren</span><span class="sxs-lookup"><span data-stu-id="5a58c-155">Publish hello output tooAzure App Service</span></span>
<span data-ttu-id="5a58c-156">In deze sectie u hoe toocreate een nieuwe API-App met behulp van hello Azure-Portal die API-App leert voor het hosten van Java-toepassingen voorbereiden en implementeren van Hallo gemaakte WAR-bestand tooAzure App Service-toorun uw nieuwe API-App.</span><span class="sxs-lookup"><span data-stu-id="5a58c-156">In this section you'll learn how toocreate a new API App using hello Azure Portal, prepare that API App for hosting Java applications, and deploy hello newly-created WAR file tooAzure App Service toorun your new API App.</span></span> 

1. <span data-ttu-id="5a58c-157">Een nieuwe API-app maken in Hallo [Azure-portal], door te klikken op Hallo **Nieuw -> Web en mobiel -> API-app** menu-item, voert u de appdetails en vervolgens te klikken op **maken**.</span><span class="sxs-lookup"><span data-stu-id="5a58c-157">Create a new API app in hello [Azure portal], by clicking hello **New -> Web + Mobile -> API app** menu item, entering your app details, and then clicking **Create**.</span></span>
   
    ![Een nieuwe API-app maken][create-api-app]
2. <span data-ttu-id="5a58c-159">Zodra de API-app is gemaakt, opent u uw app **instellingen** blade en klik vervolgens op Hallo **toepassingsinstellingen** menu-item.</span><span class="sxs-lookup"><span data-stu-id="5a58c-159">Once your API app has been created, open your app's **Settings** blade, and then click hello **Application settings** menu item.</span></span> <span data-ttu-id="5a58c-160">Selecteer Hallo meest recente Java-versies van de beschikbare opties hello, en selecteer de meest recente Tomcat Hallo Hallo **webcontainer** menu en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="5a58c-160">Select hello latest Java versions from hello available options, then select hello latest Tomcat from hello **Web container** menu, and then click **Save**.</span></span>
   
    ![Java instellen in Hallo blade API-App][set-up-java]
3. <span data-ttu-id="5a58c-162">Klik op Hallo **implementatiereferenties** menu instellingen en geef een gebruikersnaam en wachtwoord die u wenst dat toouse voor het publiceren van bestanden tooyour API-App.</span><span class="sxs-lookup"><span data-stu-id="5a58c-162">Click hello **Deployment credentials** settings menu item, and provide a username and password you wish toouse for publishing files tooyour API App.</span></span> 
   
    ![Implementatiereferenties instellen][deployment-credentials]
4. <span data-ttu-id="5a58c-164">Klik op Hallo **implementatiebron** menu instellingen.</span><span class="sxs-lookup"><span data-stu-id="5a58c-164">Click hello **Deployment source** settings menu item.</span></span> <span data-ttu-id="5a58c-165">Klik Hallo **bron kiezen** knop, selecteer Hallo **lokale Git-opslagplaats** optie en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="5a58c-165">Once there, click hello **Choose source** button, select hello **Local Git Repository** option, and then click **OK**.</span></span> <span data-ttu-id="5a58c-166">Hiermee wordt een Git-opslagplaats gemaakt die in Azure wordt uitgevoerd, met een koppeling naar uw API-app.</span><span class="sxs-lookup"><span data-stu-id="5a58c-166">This will create a Git repository running in Azure, that has an association with your API App.</span></span> <span data-ttu-id="5a58c-167">Telkens wanneer u code toohello doorvoert *master* vertakking van de Git-opslagplaats uw code gepubliceerd naar uw live API-App-exemplaar uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5a58c-167">Each time you commit code toohello *master* branch of your Git repository, your code will be published into your live running API App instance.</span></span> 
   
    ![Een nieuwe lokale Git-opslagplaats instellen][select-git-repo]
5. <span data-ttu-id="5a58c-169">Hallo nieuwe Git-opslagplaats van URL tooyour Klembord kopiëren.</span><span class="sxs-lookup"><span data-stu-id="5a58c-169">Copy hello new Git repository's URL tooyour clipboard.</span></span> <span data-ttu-id="5a58c-170">Sla de URL op, u hebt deze straks nodig.</span><span class="sxs-lookup"><span data-stu-id="5a58c-170">Save this as it will be important in a moment.</span></span> 
   
    ![Een nieuwe Git-opslagplaats voor uw app instellen][copy-git-repo-url]
6. <span data-ttu-id="5a58c-172">GIT push Hallo WAR-bestand toohello online-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="5a58c-172">Git push hello WAR file toohello online repository.</span></span> <span data-ttu-id="5a58c-173">toodo, gaat u naar Hallo **implementeren** map die u eerder hebt gemaakt, zodat u eenvoudig kunt doorvoeren Hallo code up toohello opslagplaats die wordt uitgevoerd in App Service.</span><span class="sxs-lookup"><span data-stu-id="5a58c-173">toodo this, navigate into hello **deploy** folder you created earlier so that you can easily commit hello code up toohello repository running in your App Service.</span></span> <span data-ttu-id="5a58c-174">Eenmaal u in het consolevenster Hallo en genavigeerd in Hallo map waarin Hallo webapps map bevindt, Hallo volgende Git-opdrachten toolaunch Hallo proces uitgeven en een implementatie starten.</span><span class="sxs-lookup"><span data-stu-id="5a58c-174">Once you're in hello console window and navigated into hello folder where hello webapps folder is located, issue hello following Git commands toolaunch hello process and fire off a deployment.</span></span> 
   
         git init
         git add .
         git commit -m "initial commit"
         git remote add azure [YOUR GIT URL]
         git push azure master
   
    <span data-ttu-id="5a58c-175">Als u Hallo **push** aanvraag, wordt u gevraagd om Hallo wachtwoord die u eerder voor de implementatie-referentie Hallo hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5a58c-175">Once you issue hello **push** request, you'll be asked for hello password you created for hello deployment credential earlier.</span></span> <span data-ttu-id="5a58c-176">Nadat u uw referenties invoert, ziet u uw portal weergave die Hallo update is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="5a58c-176">After you enter your credentials, you should see your portal display that hello update was deployed.</span></span>
7. <span data-ttu-id="5a58c-177">Als u nog een keer Postman toohit Hallo zojuist geïmplementeerde API-App uitgevoerd in Azure App Service gebruikt, ziet u dat Hallo gedrag consistent is en dat nu het contactpersoonsgegevens zoals verwacht, met behulp van eenvoudige code wijzigingen toohello Swagger.io ondersteunde Java-code.</span><span class="sxs-lookup"><span data-stu-id="5a58c-177">If you once again use Postman toohit hello newly-deployed API App running in Azure App Service, you'll see that hello behavior is consistent and that now it is returning contact data as expected, and using simple code changes toohello Swagger.io scaffolded Java code.</span></span> 
   
    ![Java REST API voor contactpersonen live in Azure gebruiken][postman-calling-azure-contacts]

## <a name="next-steps"></a><span data-ttu-id="5a58c-179">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5a58c-179">Next steps</span></span>
<span data-ttu-id="5a58c-180">U zou kunnen toostart met een Swagger JSON-bestand en sommige ondersteunde Java-code opgehaald uit de editor Swagger.io Hallo in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="5a58c-180">In this article, you were able toostart with a Swagger JSON file and some scaffolded Java code obtained from hello Swagger.io editor.</span></span> <span data-ttu-id="5a58c-181">Van daaruit hebben eenvoudige wijzigingen en een Git-implementatieproces geleid tot een functionele API-app, geschreven in Java.</span><span class="sxs-lookup"><span data-stu-id="5a58c-181">From there, your simple changes and a Git deploy process resulted in having a functional API app written in Java.</span></span> <span data-ttu-id="5a58c-182">Hallo volgende zelfstudie ziet u hoe te[gebruiken voor API-apps vanuit JavaScript-clients met behulp van CORS][App Service API CORS].</span><span class="sxs-lookup"><span data-stu-id="5a58c-182">hello next tutorial shows how too[consume API apps from JavaScript clients, using CORS][App Service API CORS].</span></span> <span data-ttu-id="5a58c-183">In latere zelfstudies in Hallo reeks tonen hoe tooimplement verificatie en autorisatie.</span><span class="sxs-lookup"><span data-stu-id="5a58c-183">Later tutorials in hello series show how tooimplement authentication and authorization.</span></span>

<span data-ttu-id="5a58c-184">toobuild op dit voorbeeld voor meer informatie over Hallo [opslag-SDK voor Java] toopersist Hallo JSON-blobs.</span><span class="sxs-lookup"><span data-stu-id="5a58c-184">toobuild on this sample, you can learn more about hello [Storage SDK for Java] toopersist hello JSON blobs.</span></span> <span data-ttu-id="5a58c-185">U kunt ook gebruikmaken Hallo [Java SDK voor Documentdb] toosave uw contactpersoon gegevens tooAzure Document DB.</span><span class="sxs-lookup"><span data-stu-id="5a58c-185">Or, you could use hello [Document DB Java SDK] toosave your Contact data tooAzure Document DB.</span></span> 

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="5a58c-186">Zie ook</span><span class="sxs-lookup"><span data-stu-id="5a58c-186">See Also</span></span>
<span data-ttu-id="5a58c-187">In [Azure voor Java-ontwikkelaars](/java/azure) vindt u meer informatie over het gebruik van Azure met Java.</span><span class="sxs-lookup"><span data-stu-id="5a58c-187">For more information about using Azure with Java, visit [Azure for Java developers](/java/azure).</span></span>

<!-- URL List -->

[App Service API CORS]: app-service-api-cors-consume-javascript.md
[Azure-portal]: https://portal.azure.com/
[Java SDK voor Documentdb]: ../documentdb/documentdb-java-application.md
[gratis proefversie]: https://azure.microsoft.com/pricing/free-trial/
[Git]: http://www.git-scm.com/
[Azure Java Developer Center]: /develop/java/
[Java Development Kit 8]: http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
[Jax-RS]: https://jax-rs-spec.java.net/
[Maven]: https://maven.apache.org/
[Microsoft Azure]: https://azure.microsoft.com/
[Online Swagger Editor]: http://editor2.swagger.io/
[Postman]: https://www.getpostman.com/
[opslag-SDK voor Java]:../storage/blobs/storage-java-how-to-use-blob-storage.md
[Swagger]: http://swagger.io/
[Swagger Editor]: http://editor.swagger.io/
[Visual Studio Code]: https://code.visualstudio.com

<!-- IMG List -->

[paste-json]: ./media/app-service-api-java-api-app/paste-json.png
[pasted-swagger]: ./media/app-service-api-java-api-app/pasted-swagger.png
[view-swagger-generated-docs]: ./media/app-service-api-java-api-app/view-swagger-generated-docs.png
[generate-code-menu-item]: ./media/app-service-api-java-api-app/generate-code-menu-item.png
[open-contact-model-file]: ./media/app-service-api-java-api-app/open-contact-model-file.png
[open-contact-service-code-file]: ./media/app-service-api-java-api-app/open-contact-service-code-file.png
[run-jetty-war]: ./media/app-service-api-java-api-app/run-jetty-war.png
[calling-contacts-api]: ./media/app-service-api-java-api-app/calling-contacts-api.png
[calling-specific-contact-api]: ./media/app-service-api-java-api-app/calling-specific-contact-api.png
[create-api-app]: ./media/app-service-api-java-api-app/create-api-app.png
[set-up-java]: ./media/app-service-api-java-api-app/set-up-java.png
[deployment-credentials]: ./media/app-service-api-java-api-app/deployment-credentials.png
[select-git-repo]: ./media/app-service-api-java-api-app/select-git-repo.png
[copy-git-repo-url]: ./media/app-service-api-java-api-app/copy-git-repo-url.png
[postman-calling-azure-contacts]: ./media/app-service-api-java-api-app/postman-calling-azure-contacts.png
