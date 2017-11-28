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
# <a name="how-toouse-hello-api-inspector-tootrace-calls-in-azure-api-management"></a><span data-ttu-id="99d91-103">Hoe toouse Hallo API Inspector tootrace aanroept in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="99d91-103">How toouse hello API Inspector tootrace calls in Azure API Management</span></span>
<span data-ttu-id="99d91-104">API Management biedt een API-Inspector hulpprogramma toohelp u met het opsporen en oplossen van uw API's.</span><span class="sxs-lookup"><span data-stu-id="99d91-104">API Management provides an API Inspector tool toohelp you with debugging and troubleshooting your APIs.</span></span> <span data-ttu-id="99d91-105">Hallo API Inspector via een programma kan worden gebruikt en kan ook rechtstreeks vanuit de ontwikkelaarsportal hello worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="99d91-105">hello API Inspector can be used programmatically and can also be used directly from hello developer portal.</span></span> 

<span data-ttu-id="99d91-106">Bovendien tootracing bewerkingen, API-Inspector ook traceert [beleidsexpressie](https://msdn.microsoft.com/library/azure/dn910913.aspx) evaluaties.</span><span class="sxs-lookup"><span data-stu-id="99d91-106">In addition tootracing operations, API Inspector also traces [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx) evaluations.</span></span> <span data-ttu-id="99d91-107">Zie voor een demonstratie [Cloud hebben betrekking op aflevering 177: meer API Management-functies](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) en too21:00 vooruit.</span><span class="sxs-lookup"><span data-stu-id="99d91-107">For a demonstration, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too21:00.</span></span>

<span data-ttu-id="99d91-108">Deze handleiding biedt een overzicht van het gebruik van API-Inspector.</span><span class="sxs-lookup"><span data-stu-id="99d91-108">This guide provides a walk-through of using API Inspector.</span></span>

> [!NOTE]
> <span data-ttu-id="99d91-109">API-Inspector traceringen worden alleen gegenereerd en beschikbaar gesteld voor aanvragen met abonnement sleutels die deel uitmaken van toohello [beheerder](api-management-howto-create-groups.md) account.</span><span class="sxs-lookup"><span data-stu-id="99d91-109">API Inspector traces are only generated and made available for requests containing subscription keys that belong toohello [administrator](api-management-howto-create-groups.md) account.</span></span>
> 
> 

## <span data-ttu-id="99d91-110"><a name="trace-call"></a> Gebruik API-Inspector tootrace een aanroep</span><span class="sxs-lookup"><span data-stu-id="99d91-110"><a name="trace-call"> </a> Use API Inspector tootrace a call</span></span>
<span data-ttu-id="99d91-111">API-Inspector toouse toevoegen een **ocp-apim-trace: true** header tooyour aanroepen, aanvragen en vervolgens downloaden en inspecteren Hallo trace met Hallo URL aangegeven door Hallo **ocp-apim-trace-locatie** antwoordheader.</span><span class="sxs-lookup"><span data-stu-id="99d91-111">toouse API Inspector, add an **ocp-apim-trace: true** request header tooyour operation call, and then download and inspect hello trace using hello URL indicated by hello **ocp-apim-trace-location** response header.</span></span> <span data-ttu-id="99d91-112">Dit kunt doen via programmacode en rechtstreeks vanuit de ontwikkelaarsportal Hallo kan worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="99d91-112">This can be done programatically, and can also be done directly from hello developer portal.</span></span>

<span data-ttu-id="99d91-113">Deze zelfstudie laat zien hoe toouse Hallo API Inspector tootrace bewerkingen met behulp van de basisrekenmachine-API die is geconfigureerd in Hallo Hallo [uw eerste API beheren](api-management-get-started.md) zelfstudie aan de slag.</span><span class="sxs-lookup"><span data-stu-id="99d91-113">This tutorial shows how toouse hello API Inspector tootrace operations using hello Basic Calculator API that is configured in hello [Manage your first API](api-management-get-started.md) getting started tutorial.</span></span> <span data-ttu-id="99d91-114">Als u dit nog niet hebt voltooid die zelfstudie duurt slechts enkele ogenblikken tooimport hello basisrekenmachine-API of kunt u een andere API van uw keuze zoals Hallo Echo-API.</span><span class="sxs-lookup"><span data-stu-id="99d91-114">If you haven't completed that tutorial it only takes a few moments tooimport hello Basic Calculator API, or you can use another API of your choosing such as hello Echo API.</span></span> <span data-ttu-id="99d91-115">Elk exemplaar van API Management-service wordt geleverd met een Echo-API die kan worden gebruikt tooexperiment met en meer informatie over API Management vooraf geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="99d91-115">Each API Management service instance comes pre-configured with an Echo API that can be used tooexperiment with and learn about API Management.</span></span> <span data-ttu-id="99d91-116">Hallo Echo-API retourneert terug ongeacht invoer tooit wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="99d91-116">hello Echo API returns back whatever input is sent tooit.</span></span> <span data-ttu-id="99d91-117">toouse, kunt u een HTTP-term aanroept en Hallo retourwaarde gewoon worden wat u hebt verzonden.</span><span class="sxs-lookup"><span data-stu-id="99d91-117">toouse it, you can invoke any HTTP verb, and hello return value will simply be what you sent.</span></span> 

<span data-ttu-id="99d91-118">tooget gestart, klikt u op **ontwikkelaarsportal** in hello Azure-Portal voor uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="99d91-118">tooget started, click **Developer portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="99d91-119">Bewerkingen kunnen rechtstreeks vanuit het Hallo-portal voor ontwikkelaars die een handige manier tooview biedt worden aangeroepen en Hallo bewerkingen van een API testen.</span><span class="sxs-lookup"><span data-stu-id="99d91-119">Operations can be called directly from hello developer portal which provides a convenient way tooview and test hello operations of an API.</span></span>

> <span data-ttu-id="99d91-120">Als u nog een exemplaar van API Management-service hebt gemaakt, Zie [API Management service-exemplaar maken] [ Create an API Management service instance] in Hallo [aan de slag met Azure API Management] [ Get started with Azure API Management] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="99d91-120">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

![API Management-portal voor ontwikkelaars][api-management-developer-portal-menu]

<span data-ttu-id="99d91-122">Klik op **API's** van Hallo bovenste menu en klik vervolgens op **basisrekenmachine**.</span><span class="sxs-lookup"><span data-stu-id="99d91-122">Click **APIs** from hello top menu, and then click **Basic Calculator**.</span></span>

![Echo-API][api-management-api]

<span data-ttu-id="99d91-124">Klik op **Try it** tootry hello **twee gehele getallen toevoegen** bewerking.</span><span class="sxs-lookup"><span data-stu-id="99d91-124">Click **Try it** tootry hello **Add two integers** operation.</span></span>

![Probeer het nu][api-management-open-console]

<span data-ttu-id="99d91-126">Voorkomen dat Hallo standaardparameterwaarden en selecteer Hallo abonnementssleutel voor Hallo product dat u wilt toouse hello **abonnementssleutel** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="99d91-126">Keep hello default parameter values, and select hello subscription key for hello product you want toouse from hello **subscription-key** drop-down.</span></span>

<span data-ttu-id="99d91-127">Standaard in Hallo developer portal Hallo **Ocp-Apim-Trace** header is al ingesteld te**true**.</span><span class="sxs-lookup"><span data-stu-id="99d91-127">By default in hello developer portal hello **Ocp-Apim-Trace** header is already set too**true**.</span></span> <span data-ttu-id="99d91-128">Deze header configureert u of er een tracering wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="99d91-128">This header configures whether or not a trace is generated.</span></span>

![Verzenden][api-management-http-get]

<span data-ttu-id="99d91-130">Klik op **verzenden** tooinvoke Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="99d91-130">Click **Send** tooinvoke hello operation.</span></span>

![Verzenden][api-management-send-results]

<span data-ttu-id="99d91-132">In het antwoord Hallo headers niet een **ocp-apim-trace-locatie** met een waarde van een vergelijkbare toohello voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="99d91-132">In hello response headers will be an **ocp-apim-trace-location** with a value similar toohello following example.</span></span>

```
ocp-apim-trace-location : https://contosoltdxw7zagdfsprykd.blob.core.windows.net/apiinspectorcontainer/ZW3e23NsW4wQyS-SHjS0Og2-2?sv=2013-08-15&sr=b&sig=Mgx7cMHsLmVDv%2B%2BSzvg3JR8qGTHoOyIAV7xDsZbF7%2Bk%3D&se=2014-05-04T21%3A00%3A13Z&sp=r&verify_guid=a56a17d83de04fcb8b9766df38514742
```

<span data-ttu-id="99d91-133">Hallo-tracering kan worden gedownload vanaf Hallo opgegeven locatie en gecontroleerd, zoals wordt beschreven in de volgende stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="99d91-133">hello trace can be downloaded from hello specified location and reviewed as demonstrated in hello next step.</span></span> <span data-ttu-id="99d91-134">Houd er rekening mee dat alleen Hallo laatste 100 logboekvermeldingen worden opgeslagen en logboeklocaties opnieuw worden gebruikt in de draaihoek.</span><span class="sxs-lookup"><span data-stu-id="99d91-134">Note that only hello last 100 log entries are stored and log locations are reused in rotation.</span></span> <span data-ttu-id="99d91-135">In dat geval als u meer dan 100 aanroept met tracering ingeschakeld begint u met het uiteindelijk Hallo eerste traceringen erin wordt overschreven.</span><span class="sxs-lookup"><span data-stu-id="99d91-135">So if you make more than 100 calls with tracing enabled you will eventually start overwriting hello first traces in place.</span></span>

## <span data-ttu-id="99d91-136"><a name="inspect-trace"></a>Hello trace controleren</span><span class="sxs-lookup"><span data-stu-id="99d91-136"><a name="inspect-trace"> </a>Inspect hello trace</span></span>
<span data-ttu-id="99d91-137">tooreview hello waarden in Hallo-tracering Hallo traceringsbestand downloaden van Hallo **ocp-apim-trace-locatie** URL.</span><span class="sxs-lookup"><span data-stu-id="99d91-137">tooreview hello values in hello trace, download hello trace file from hello **ocp-apim-trace-location** URL.</span></span> <span data-ttu-id="99d91-138">Dit is een tekstbestand in JSON-indeling en bevat vermeldingen vergelijkbare toohello voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="99d91-138">It is a text file in JSON format, and contains entries similar toohello following example.</span></span>

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

## <span data-ttu-id="99d91-139"><a name="next-steps"> </a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="99d91-139"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="99d91-140">Bekijk een demo voor tracering van beleidsexpressies in [Cloud hebben betrekking op aflevering 177: meer API Management-functies](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/).</span><span class="sxs-lookup"><span data-stu-id="99d91-140">Watch a demo of tracing policy expressions in [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/).</span></span> <span data-ttu-id="99d91-141">Vooruit too21:00 toosee Hallo demo.</span><span class="sxs-lookup"><span data-stu-id="99d91-141">Fast-forward too21:00 toosee hello demo.</span></span>

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




