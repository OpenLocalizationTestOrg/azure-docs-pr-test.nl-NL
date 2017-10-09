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
# <a name="build-and-deploy-a-java-api-app-in-azure-app-service"></a>Een Java API-app bouwen en implementeren in Azure App Service
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

Deze zelfstudie laat zien hoe toocreate een Java-toepassing en implementeer deze tooAzure App Service API-Apps met behulp van [Git]. Hallo-instructies in deze zelfstudie kunnen worden uitgevoerd op elk besturingssysteem waarmee Java uitgevoerd. Hallo-code in deze zelfstudie wordt gebouwd met [Maven]. [Jax-RS] gebruikte toocreate hello RESTful-Service is en is gegenereerd op basis van Hallo [Swagger] metagegevens specificatie Hallo met [Swagger Editor].

## <a name="prerequisites"></a>Vereisten
1. [Java Development Kit 8] \(of hoger)
2. [Maven] is geïnstalleerd op uw ontwikkelcomputer
3. [Git] is geïnstalleerd op uw ontwikkelcomputer
4. Een betaald of [gratis proefversie] abonnement te[Microsoft Azure]
5. Een HTTP-testtoepassing zoals [Postman]

## <a name="scaffold-hello-api-using-swaggerio"></a>Scaffold hello API met behulp van Swagger.IO
Hallo online-editor swagger.io kunt u Swagger JSON- of YAML-code die Hallo-structuur van uw API vertegenwoordigt invoeren. Zodra u Hallo API oppervlak ontworpen hebt, kunt u code voor verschillende platforms en frameworks exporteren. In de volgende sectie hello, Hallo die code gewijzigde tooinclude mock-functionaliteit niet. 

Deze demonstratie begint met een Swagger JSON-hoofdtekst die u in de editor swagger.io hello, wordt plakken die wordt vervolgens worden gebruikte toogenerate code waarbij gebruik wordt gemaakt van JAX-RS tooaccess een REST-API-eindpunt. Vervolgens bewerkt u Hallo die code tooreturn Hiermee mock-gegevens, een REST-API die is gebouwd op een mechanisme simuleren.  

1. Hallo volgende Swagger JSON-code tooyour Klembord kopiëren:
   
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
2. Navigeer toohello [Online Swagger Editor]. Klik Hallo **File -> Paste JSON** menu-item.
   
    ![Menuopdracht Paste JSON][paste-json]
3. Plak in Hallo contactpersonen lijst API Swagger JSON u eerder hebt gekopieerd. 
   
    ![JSON-code plakken in Swagger][pasted-swagger]
4. Hallo-documentatie pagina's en API-overzicht weergegeven in het Hallo-editor weergeven. 
   
    ![Door Swagger gegenereerde documenten weergeven][view-swagger-generated-docs]
5. Selecteer Hallo **Generate Server -> JAX-RS** menu optie tooscaffold Hallo servercode u later tooadd mock-implementatie gaat bewerken. 
   
    ![Menuopdracht Generate Code][generate-code-menu-item]
   
    Zodra het Hallo-code is gegenereerd, is het hebt dat u een ZIP-bestand toodownload worden opgegeven. Dit bestand bevat Hallo-code die door de Swagger-codegenerator Hallo en alle gekoppelde bouwscripts. Pak Hallo hele bibliotheek tooa map op uw ontwikkelwerkstation. 

## <a name="edit-hello-code-tooadd-api-implementation"></a>Hallo Code tooadd API implementatie bewerken
In deze sectie zult u Hallo Swagger gegenereerde code serverimplementatie vervangen door uw eigen aangepaste code. Hallo nieuwe code wordt een Matrixlijst met entiteiten toohello aanroepende client geretourneerd. 

1. Open Hallo *Contact.java* modelbestand dat in Hallo bevindt zich *src/gen/java/io/swagger/model* map met [Visual Studio Code] of uw favoriete teksteditor. 
   
    ![Modelbestand voor contactpersonen openen][open-contact-model-file]
2. Toevoegen van de volgende constructor binnen Hallo Hallo **Contact** klasse. 
   
        public Contact(Integer id, String name, String email) 
        {
            this.id = id;
            this.name = name;
            this.emailAddress = email;
        }
3. Open Hallo *ContactsApiServiceImpl.java* service-implementatiebestand dat in Hallo bevindt zich *src/main/java/io/swagger/api/impl* map met [Visual Studio Code]of uw favoriete teksteditor.
   
    ![Servicecodebestand voor contactpersonen openen][open-contact-service-code-file]
4. Hallo-code in Hallo bestand overschrijven met deze nieuwe code tooadd een code toohello mock-implementatie. 
   
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
5. Open een opdrachtprompt en wijzig directory toohello hoofdmap van uw toepassing.
6. Hallo volgende Maven-opdracht toobuild Hallo code uitvoeren en voer dit lokaal met behulp van Hallo Jetty-app-server. 
   
        mvn package jetty:run
7. U ziet Hallo-opdrachtvenster weer dat Jetty uw code via poort 8080 is gestart. 
   
    ![Servicecodebestand voor contactpersonen openen][run-jetty-war]
8. Gebruik [Postman] toomake een aanvraag toohello 'ophalen van alle contactpersonen' API-methode via http://localhost: 8080/api/contacts.
   
    ![Hallo API voor contactpersonen aanroepen][calling-contacts-api]
9. Gebruik [Postman] toomake een aanvraag toohello 'ophalen van een specifieke contactpersoon' API-methode zich bevindt op http://localhost: 8080/api/contacts/2.
   
    ![Hallo API voor contactpersonen aanroepen][calling-specific-contact-api]
10. Bouw ten slotte Hallo Java WAR (webarchief)-bestand door het uitvoeren van Hallo volgende Maven-opdracht in de console. 
    
         mvn package war:war
11. Als Hallo WAR-bestand is gebouwd, wordt deze geplaatst in Hallo **doel** map. Navigeer naar Hallo **doel** map en wijzig de naam Hallo u WAR-bestand te**ROOT.war**. (Zorg ervoor dat Hallo hoofdlettergebruik overeenkomt met deze indeling).
    
          rename swagger-jaxrs-server-1.0.0.war ROOT.war
12. Ten slotte uitvoeren Hallo volgende opdrachten uit Hallo hoofdmap van uw toepassing toocreate een **implementeren** tooAzure map toouse toodeploy Hallo WAR-bestand. 
    
          mkdir deploy
          mkdir deploy\webapps
          copy target\ROOT.war deploy\webapps
          cd deploy

## <a name="publish-hello-output-tooazure-app-service"></a>Hallo uitvoer tooAzure App Service publiceren
In deze sectie u hoe toocreate een nieuwe API-App met behulp van hello Azure-Portal die API-App leert voor het hosten van Java-toepassingen voorbereiden en implementeren van Hallo gemaakte WAR-bestand tooAzure App Service-toorun uw nieuwe API-App. 

1. Een nieuwe API-app maken in Hallo [Azure-portal], door te klikken op Hallo **Nieuw -> Web en mobiel -> API-app** menu-item, voert u de appdetails en vervolgens te klikken op **maken**.
   
    ![Een nieuwe API-app maken][create-api-app]
2. Zodra de API-app is gemaakt, opent u uw app **instellingen** blade en klik vervolgens op Hallo **toepassingsinstellingen** menu-item. Selecteer Hallo meest recente Java-versies van de beschikbare opties hello, en selecteer de meest recente Tomcat Hallo Hallo **webcontainer** menu en klik vervolgens op **opslaan**.
   
    ![Java instellen in Hallo blade API-App][set-up-java]
3. Klik op Hallo **implementatiereferenties** menu instellingen en geef een gebruikersnaam en wachtwoord die u wenst dat toouse voor het publiceren van bestanden tooyour API-App. 
   
    ![Implementatiereferenties instellen][deployment-credentials]
4. Klik op Hallo **implementatiebron** menu instellingen. Klik Hallo **bron kiezen** knop, selecteer Hallo **lokale Git-opslagplaats** optie en klik vervolgens op **OK**. Hiermee wordt een Git-opslagplaats gemaakt die in Azure wordt uitgevoerd, met een koppeling naar uw API-app. Telkens wanneer u code toohello doorvoert *master* vertakking van de Git-opslagplaats uw code gepubliceerd naar uw live API-App-exemplaar uitgevoerd. 
   
    ![Een nieuwe lokale Git-opslagplaats instellen][select-git-repo]
5. Hallo nieuwe Git-opslagplaats van URL tooyour Klembord kopiëren. Sla de URL op, u hebt deze straks nodig. 
   
    ![Een nieuwe Git-opslagplaats voor uw app instellen][copy-git-repo-url]
6. GIT push Hallo WAR-bestand toohello online-opslagplaats. toodo, gaat u naar Hallo **implementeren** map die u eerder hebt gemaakt, zodat u eenvoudig kunt doorvoeren Hallo code up toohello opslagplaats die wordt uitgevoerd in App Service. Eenmaal u in het consolevenster Hallo en genavigeerd in Hallo map waarin Hallo webapps map bevindt, Hallo volgende Git-opdrachten toolaunch Hallo proces uitgeven en een implementatie starten. 
   
         git init
         git add .
         git commit -m "initial commit"
         git remote add azure [YOUR GIT URL]
         git push azure master
   
    Als u Hallo **push** aanvraag, wordt u gevraagd om Hallo wachtwoord die u eerder voor de implementatie-referentie Hallo hebt gemaakt. Nadat u uw referenties invoert, ziet u uw portal weergave die Hallo update is geïmplementeerd.
7. Als u nog een keer Postman toohit Hallo zojuist geïmplementeerde API-App uitgevoerd in Azure App Service gebruikt, ziet u dat Hallo gedrag consistent is en dat nu het contactpersoonsgegevens zoals verwacht, met behulp van eenvoudige code wijzigingen toohello Swagger.io ondersteunde Java-code. 
   
    ![Java REST API voor contactpersonen live in Azure gebruiken][postman-calling-azure-contacts]

## <a name="next-steps"></a>Volgende stappen
U zou kunnen toostart met een Swagger JSON-bestand en sommige ondersteunde Java-code opgehaald uit de editor Swagger.io Hallo in dit artikel. Van daaruit hebben eenvoudige wijzigingen en een Git-implementatieproces geleid tot een functionele API-app, geschreven in Java. Hallo volgende zelfstudie ziet u hoe te[gebruiken voor API-apps vanuit JavaScript-clients met behulp van CORS][App Service API CORS]. In latere zelfstudies in Hallo reeks tonen hoe tooimplement verificatie en autorisatie.

toobuild op dit voorbeeld voor meer informatie over Hallo [opslag-SDK voor Java] toopersist Hallo JSON-blobs. U kunt ook gebruikmaken Hallo [Java SDK voor Documentdb] toosave uw contactpersoon gegevens tooAzure Document DB. 

<a name="see-also"></a>

## <a name="see-also"></a>Zie ook
In [Azure voor Java-ontwikkelaars](/java/azure) vindt u meer informatie over het gebruik van Azure met Java.

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
