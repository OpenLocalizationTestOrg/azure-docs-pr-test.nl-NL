---
title: aaaTrace aanroepen met API-Inspector - Azure API Management | Microsoft Docs
description: Meer informatie over hoe tootrace aanroepen met Hallo API-Inspector in Azure API Management.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 4b222327-c8a4-4f33-9a06-adff2a9834d9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: b0c401caa8da1b789f6cfe5edf97a5f118d78f26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-api-inspector-tootrace-calls-in-azure-api-management"></a>Hoe toouse Hallo API Inspector tootrace aanroept in Azure API Management
API Management biedt een API-Inspector hulpprogramma toohelp u met het opsporen en oplossen van uw API's. Hallo API Inspector via een programma kan worden gebruikt en kan ook rechtstreeks vanuit de ontwikkelaarsportal hello worden gebruikt. 

Bovendien tootracing bewerkingen, API-Inspector ook traceert [beleidsexpressie](https://msdn.microsoft.com/library/azure/dn910913.aspx) evaluaties. Zie voor een demonstratie [Cloud hebben betrekking op aflevering 177: meer API Management-functies](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) en too21:00 vooruit.

Deze handleiding biedt een overzicht van het gebruik van API-Inspector.

> [!NOTE]
> API-Inspector traceringen worden alleen gegenereerd en beschikbaar gesteld voor aanvragen met abonnement sleutels die deel uitmaken van toohello [beheerder](api-management-howto-create-groups.md) account.
> 
> 

## <a name="trace-call"></a> Gebruik API-Inspector tootrace een aanroep
API-Inspector toouse toevoegen een **ocp-apim-trace: true** header tooyour aanroepen, aanvragen en vervolgens downloaden en inspecteren Hallo trace met Hallo URL aangegeven door Hallo **ocp-apim-trace-locatie** antwoordheader. Dit kunt doen via programmacode en rechtstreeks vanuit de ontwikkelaarsportal Hallo kan worden uitgevoerd.

Deze zelfstudie laat zien hoe toouse Hallo API Inspector tootrace bewerkingen met behulp van de basisrekenmachine-API die is geconfigureerd in Hallo Hallo [uw eerste API beheren](api-management-get-started.md) zelfstudie aan de slag. Als u dit nog niet hebt voltooid die zelfstudie duurt slechts enkele ogenblikken tooimport hello basisrekenmachine-API of kunt u een andere API van uw keuze zoals Hallo Echo-API. Elk exemplaar van API Management-service wordt geleverd met een Echo-API die kan worden gebruikt tooexperiment met en meer informatie over API Management vooraf geconfigureerd. Hallo Echo-API retourneert terug ongeacht invoer tooit wordt verzonden. toouse, kunt u een HTTP-term aanroept en Hallo retourwaarde gewoon worden wat u hebt verzonden. 

tooget gestart, klikt u op **ontwikkelaarsportal** in hello Azure-Portal voor uw API Management-service. Bewerkingen kunnen rechtstreeks vanuit het Hallo-portal voor ontwikkelaars die een handige manier tooview biedt worden aangeroepen en Hallo bewerkingen van een API testen.

> Als u nog een exemplaar van API Management-service hebt gemaakt, Zie [API Management service-exemplaar maken] [ Create an API Management service instance] in Hallo [aan de slag met Azure API Management] [ Get started with Azure API Management] zelfstudie.
> 
> 

![API Management-portal voor ontwikkelaars][api-management-developer-portal-menu]

Klik op **API's** van Hallo bovenste menu en klik vervolgens op **basisrekenmachine**.

![Echo-API][api-management-api]

Klik op **Try it** tootry hello **twee gehele getallen toevoegen** bewerking.

![Probeer het nu][api-management-open-console]

Voorkomen dat Hallo standaardparameterwaarden en selecteer Hallo abonnementssleutel voor Hallo product dat u wilt toouse hello **abonnementssleutel** vervolgkeuzelijst.

Standaard in Hallo developer portal Hallo **Ocp-Apim-Trace** header is al ingesteld te**true**. Deze header configureert u of er een tracering wordt gegenereerd.

![Verzenden][api-management-http-get]

Klik op **verzenden** tooinvoke Hallo-bewerking.

![Verzenden][api-management-send-results]

In het antwoord Hallo headers niet een **ocp-apim-trace-locatie** met een waarde van een vergelijkbare toohello voorbeeld te volgen.

```
ocp-apim-trace-location : https://contosoltdxw7zagdfsprykd.blob.core.windows.net/apiinspectorcontainer/ZW3e23NsW4wQyS-SHjS0Og2-2?sv=2013-08-15&sr=b&sig=Mgx7cMHsLmVDv%2B%2BSzvg3JR8qGTHoOyIAV7xDsZbF7%2Bk%3D&se=2014-05-04T21%3A00%3A13Z&sp=r&verify_guid=a56a17d83de04fcb8b9766df38514742
```

Hallo-tracering kan worden gedownload vanaf Hallo opgegeven locatie en gecontroleerd, zoals wordt beschreven in de volgende stap Hallo. Houd er rekening mee dat alleen Hallo laatste 100 logboekvermeldingen worden opgeslagen en logboeklocaties opnieuw worden gebruikt in de draaihoek. In dat geval als u meer dan 100 aanroept met tracering ingeschakeld begint u met het uiteindelijk Hallo eerste traceringen erin wordt overschreven.

## <a name="inspect-trace"></a>Hello trace controleren
tooreview hello waarden in Hallo-tracering Hallo traceringsbestand downloaden van Hallo **ocp-apim-trace-locatie** URL. Dit is een tekstbestand in JSON-indeling en bevat vermeldingen vergelijkbare toohello voorbeeld te volgen.

```json
{
    "traceId": "abcd8ea63d134c1fabe6371566c7cbea",
    "traceEntries": {
        "inbound": [
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.2998610Z",
                "elapsed": "00:00:00.0725926",
                "data": {
                    "request": {
                        "method": "GET",
                        "url": "https://contoso5.azure-api.net/calc/add?a=51&b=49",
                        "headers": [
                            {
                                "name": "Ocp-Apim-Subscription-Key",
                                "value": "5d7c41af64a44a68a2ea46580d271a59"
                            },
                            {
                                "name": "Connection",
                                "value": "Keep-Alive"
                            },
                            {
                                "name": "Host",
                                "value": "contoso5.azure-api.net"
                            }
                        ]
                    }
                }
            },
            {
                "source": "mapper",
                "timestamp": "2015-06-23T19:51:35.2998610Z",
                "elapsed": "00:00:00.0726213",
                "data": {
                    "configuration": {
                        "api": {
                            "from": "/calc",
                            "to": {
                                "scheme": "http",
                                "host": "calcapi.cloudapp.net",
                                "port": 80,
                                "path": "/api",
                                "queryString": "",
                                "query": {},
                                "isDefaultPort": true
                            }
                        },
                        "operation": {
                            "method": "GET",
                            "uriTemplate": "/add?a={a}&b={b}"
                        },
                        "user": {
                            "id": 1,
                            "groups": [
                                "Administrators",
                                "Developers"
                            ]
                        },
                        "product": {
                            "id": 1
                        }
                    }
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.2998610Z",
                "elapsed": "00:00:00.0727522",
                "data": {
                    "message": "Request is being forwarded toohello backend service.",
                    "request": {
                        "method": "GET",
                        "url": "http://calcapi.cloudapp.net/api/add?a=51&b=49",
                        "headers": [
                            {
                                "name": "Ocp-Apim-Subscription-Key",
                                "value": "5d7c41af64a44a68a2ea46580d271a59"
                            },
                            {
                                "name": "X-Forwarded-For",
                                "value": "33.52.215.35"
                            }
                        ]
                    }
                }
            }
        ],
        "outbound": [
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1960601",
                "data": {
                    "response": {
                        "status": {
                            "code": 200,
                            "reason": "OK"
                        },
                        "headers": [
                            {
                                "name": "Pragma",
                                "value": "no-cache"
                            },
                            {
                                "name": "Content-Length",
                                "value": "124"
                            },
                            {
                                "name": "Cache-Control",
                                "value": "no-cache"
                            },
                            {
                                "name": "Content-Type",
                                "value": "application/xml; charset=utf-8"
                            },
                            {
                                "name": "Date",
                                "value": "Tue, 23 Jun 2015 19:51:35 GMT"
                            },
                            {
                                "name": "Expires",
                                "value": "-1"
                            },
                            {
                                "name": "Server",
                                "value": "Microsoft-IIS/8.5"
                            },
                            {
                                "name": "X-AspNet-Version",
                                "value": "4.0.30319"
                            },
                            {
                                "name": "X-Powered-By",
                                "value": "ASP.NET"
                            }
                        ]
                    }
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1961112",
                "data": {
                    "message": "Response headers have been sent toohello caller. Starting toostream hello response body."
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1963155",
                "data": {
                    "message": "Response body streaming toohello caller is complete."
                }
            }
        ]
    }
}
```

## <a name="next-steps"> </a>Volgende stappen
* Bekijk een demo voor tracering van beleidsexpressies in [Cloud hebben betrekking op aflevering 177: meer API Management-functies](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/). Vooruit too21:00 toosee Hallo demo.

> [!VIDEO https://channel9.msdn.com/Shows/Cloud+Cover/Episode-177-More-API-Management-Features-with-Vlad-Vinogradsky/player]
> 
> 

[Use API Inspector tootrace a call]: #trace-call
[Inspect hello trace]: #inspect-trace
[Next steps]: #next-steps

[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[Responses]: api-management-howto-add-operations.md#responses
[How create and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Azure Classic Portal]: https://manage.windowsazure.com/


[api-management-developer-portal-menu]: ./media/api-management-howto-api-inspector/api-management-developer-portal-menu.png
[api-management-api]: ./media/api-management-howto-api-inspector/api-management-api.png
[api-management-echo-api-get]: ./media/api-management-howto-api-inspector/api-management-echo-api-get.png
[api-management-developer-key]: ./media/api-management-howto-api-inspector/api-management-developer-key.png
[api-management-open-console]: ./media/api-management-howto-api-inspector/api-management-open-console.png
[api-management-http-get]: ./media/api-management-howto-api-inspector/api-management-http-get.png
[api-management-send-results]: ./media/api-management-howto-api-inspector/api-management-send-results.png




