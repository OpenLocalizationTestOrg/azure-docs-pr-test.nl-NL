---
title: Trace-aanroepen met API-Inspector - Azure API Management | Microsoft Docs
description: Informatie over het traceren van aanroepen met behulp van de API-Inspector in Azure API Management.
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
ms.openlocfilehash: a9d4d3be7f046af975f6dc25670070204848588c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-api-inspector-to-trace-calls-in-azure-api-management"></a><span data-ttu-id="f1cbb-103">Het gebruik van de API-Inspector te traceren aanroepen in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="f1cbb-103">How to use the API Inspector to trace calls in Azure API Management</span></span>
<span data-ttu-id="f1cbb-104">API Management biedt een API-Inspector-hulpprogramma om u te helpen bij het opsporen en oplossen van uw API's.</span><span class="sxs-lookup"><span data-stu-id="f1cbb-104">API Management provides an API Inspector tool to help you with debugging and troubleshooting your APIs.</span></span> <span data-ttu-id="f1cbb-105">De API-Inspector via een programma kan worden gebruikt en kan ook rechtstreeks vanuit de portal voor ontwikkelaars worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f1cbb-105">The API Inspector can be used programmatically and can also be used directly from the developer portal.</span></span> 

<span data-ttu-id="f1cbb-106">Naast de tracering bewerkingen, API-Inspector ook traceert [beleidsexpressie](https://msdn.microsoft.com/library/azure/dn910913.aspx) evaluaties.</span><span class="sxs-lookup"><span data-stu-id="f1cbb-106">In addition to tracing operations, API Inspector also traces [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx) evaluations.</span></span> <span data-ttu-id="f1cbb-107">Zie voor een demonstratie [Cloud hebben betrekking op aflevering 177: meer API Management-functies](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) en vooruit tot 21:00.</span><span class="sxs-lookup"><span data-stu-id="f1cbb-107">For a demonstration, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 21:00.</span></span>

<span data-ttu-id="f1cbb-108">Deze handleiding biedt een overzicht van het gebruik van API-Inspector.</span><span class="sxs-lookup"><span data-stu-id="f1cbb-108">This guide provides a walk-through of using API Inspector.</span></span>

> [!NOTE]
> <span data-ttu-id="f1cbb-109">API-Inspector traceringen worden alleen gegenereerd en beschikbaar gesteld voor aanvragen met abonnement sleutels die deel uitmaken van de [beheerder](api-management-howto-create-groups.md) account.</span><span class="sxs-lookup"><span data-stu-id="f1cbb-109">API Inspector traces are only generated and made available for requests containing subscription keys that belong to the [administrator](api-management-howto-create-groups.md) account.</span></span>
> 
> 

## <span data-ttu-id="f1cbb-110"><a name="trace-call"></a> API-Inspector gebruikt om te traceren, een aanroep</span><span class="sxs-lookup"><span data-stu-id="f1cbb-110"><a name="trace-call"> </a> Use API Inspector to trace a call</span></span>
<span data-ttu-id="f1cbb-111">Voor het gebruik van API-Inspector toevoegen een **ocp-apim-trace: true** aanvraagheader voor uw bewerking gesprek, en vervolgens downloaden en controleren van de tracering via de URL die is aangegeven door de **ocp-apim-trace-locatie** antwoordheader.</span><span class="sxs-lookup"><span data-stu-id="f1cbb-111">To use API Inspector, add an **ocp-apim-trace: true** request header to your operation call, and then download and inspect the trace using the URL indicated by the **ocp-apim-trace-location** response header.</span></span> <span data-ttu-id="f1cbb-112">Dit via programmacode kan worden uitgevoerd en is ook mogelijk rechtstreeks vanuit de portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="f1cbb-112">This can be done programatically, and can also be done directly from the developer portal.</span></span>

<span data-ttu-id="f1cbb-113">Deze zelfstudie laat zien hoe u de API-Inspector trace-bewerkingen met behulp van de basisrekenmachine-API die is geconfigureerd in de [uw eerste API beheren](api-management-get-started.md) zelfstudie aan de slag.</span><span class="sxs-lookup"><span data-stu-id="f1cbb-113">This tutorial shows how to use the API Inspector to trace operations using the Basic Calculator API that is configured in the [Manage your first API](api-management-get-started.md) getting started tutorial.</span></span> <span data-ttu-id="f1cbb-114">Als u dit nog niet hebt voltooid die zelfstudie duurt slechts enkele ogenblikken voor het importeren van de basisrekenmachine-API of kunt u een andere API keuze op, zoals de Echo-API.</span><span class="sxs-lookup"><span data-stu-id="f1cbb-114">If you haven't completed that tutorial it only takes a few moments to import the Basic Calculator API, or you can use another API of your choosing such as the Echo API.</span></span> <span data-ttu-id="f1cbb-115">Elk service-exemplaar van API Management wordt al geconfigureerd geleverd met een Echo-API die kan worden gebruikt om te experimenteren met API Management en hier meer over te leren.</span><span class="sxs-lookup"><span data-stu-id="f1cbb-115">Each API Management service instance comes pre-configured with an Echo API that can be used to experiment with and learn about API Management.</span></span> <span data-ttu-id="f1cbb-116">De Echo-API retourneert terug ongeacht invoer is verzonden.</span><span class="sxs-lookup"><span data-stu-id="f1cbb-116">The Echo API returns back whatever input is sent to it.</span></span> <span data-ttu-id="f1cbb-117">Als u wilt gebruiken, kunt u een HTTP-term aanroept en de retourwaarde worden gewoon wat u hebt verzonden.</span><span class="sxs-lookup"><span data-stu-id="f1cbb-117">To use it, you can invoke any HTTP verb, and the return value will simply be what you sent.</span></span> 

<span data-ttu-id="f1cbb-118">Om te beginnen, klikt u op **ontwikkelaarsportal** in de Azure-Portal voor uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="f1cbb-118">To get started, click **Developer portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="f1cbb-119">Bewerkingen kunnen rechtstreeks vanuit de portal voor ontwikkelaars die biedt een handige manier om te bekijken en testen van de bewerkingen van een API worden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f1cbb-119">Operations can be called directly from the developer portal which provides a convenient way to view and test the operations of an API.</span></span>

> <span data-ttu-id="f1cbb-120">Als u nog een exemplaar van API Management-service hebt gemaakt, Zie [API Management service-exemplaar maken] [ Create an API Management service instance] in de [aan de slag met Azure API Management] [ Get started with Azure API Management] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="f1cbb-120">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

![API Management-portal voor ontwikkelaars][api-management-developer-portal-menu]

<span data-ttu-id="f1cbb-122">Klik op **API's** van het bovenste menu en klik op **basisrekenmachine**.</span><span class="sxs-lookup"><span data-stu-id="f1cbb-122">Click **APIs** from the top menu, and then click **Basic Calculator**.</span></span>

![Echo-API][api-management-api]

<span data-ttu-id="f1cbb-124">Klik op **Try it** om te proberen de **twee gehele getallen toevoegen** bewerking.</span><span class="sxs-lookup"><span data-stu-id="f1cbb-124">Click **Try it** to try the **Add two integers** operation.</span></span>

![Probeer het nu][api-management-open-console]

<span data-ttu-id="f1cbb-126">Gebruik de standaardwaarde parameterwaarden en selecteert u de sleutel van het abonnement voor het product dat u gebruiken wilt vanaf de **abonnementssleutel** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="f1cbb-126">Keep the default parameter values, and select the subscription key for the product you want to use from the **subscription-key** drop-down.</span></span>

<span data-ttu-id="f1cbb-127">In de portal voor ontwikkelaars standaard de **Ocp-Apim-Trace** header is al ingesteld op **true**.</span><span class="sxs-lookup"><span data-stu-id="f1cbb-127">By default in the developer portal the **Ocp-Apim-Trace** header is already set to **true**.</span></span> <span data-ttu-id="f1cbb-128">Deze header configureert u of er een tracering wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="f1cbb-128">This header configures whether or not a trace is generated.</span></span>

![Verzenden][api-management-http-get]

<span data-ttu-id="f1cbb-130">Klik op **verzenden** aanroepen van de bewerking.</span><span class="sxs-lookup"><span data-stu-id="f1cbb-130">Click **Send** to invoke the operation.</span></span>

![Verzenden][api-management-send-results]

<span data-ttu-id="f1cbb-132">In het antwoord headers is een **ocp-apim-trace-locatie** met een waarde gelijkaardig aan het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="f1cbb-132">In the response headers will be an **ocp-apim-trace-location** with a value similar to the following example.</span></span>

```
ocp-apim-trace-location : https://contosoltdxw7zagdfsprykd.blob.core.windows.net/apiinspectorcontainer/ZW3e23NsW4wQyS-SHjS0Og2-2?sv=2013-08-15&sr=b&sig=Mgx7cMHsLmVDv%2B%2BSzvg3JR8qGTHoOyIAV7xDsZbF7%2Bk%3D&se=2014-05-04T21%3A00%3A13Z&sp=r&verify_guid=a56a17d83de04fcb8b9766df38514742
```

<span data-ttu-id="f1cbb-133">De tracering kan worden gedownload vanaf de opgegeven locatie en gecontroleerd, zoals wordt beschreven in de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="f1cbb-133">The trace can be downloaded from the specified location and reviewed as demonstrated in the next step.</span></span> <span data-ttu-id="f1cbb-134">Houd er rekening mee dat alleen de laatste 100 logboekvermeldingen worden opgeslagen en logboeklocaties opnieuw worden gebruikt in de draaihoek.</span><span class="sxs-lookup"><span data-stu-id="f1cbb-134">Note that only the last 100 log entries are stored and log locations are reused in rotation.</span></span> <span data-ttu-id="f1cbb-135">In dat geval als u meer dan 100 aanroept met tracering ingeschakeld begint u met het uiteindelijk wordt overschreven de eerste traceringen aanwezig.</span><span class="sxs-lookup"><span data-stu-id="f1cbb-135">So if you make more than 100 calls with tracing enabled you will eventually start overwriting the first traces in place.</span></span>

## <span data-ttu-id="f1cbb-136"><a name="inspect-trace"></a>Inspecteer de tracering</span><span class="sxs-lookup"><span data-stu-id="f1cbb-136"><a name="inspect-trace"> </a>Inspect the trace</span></span>
<span data-ttu-id="f1cbb-137">Om de waarden in de tracering controleren, downloaden de traceringsbestand van de **ocp-apim-trace-locatie** URL.</span><span class="sxs-lookup"><span data-stu-id="f1cbb-137">To review the values in the trace, download the trace file from the **ocp-apim-trace-location** URL.</span></span> <span data-ttu-id="f1cbb-138">Er is een tekstbestand in JSON-indeling en vermeldingen die lijken op het volgende voorbeeld bevat.</span><span class="sxs-lookup"><span data-stu-id="f1cbb-138">It is a text file in JSON format, and contains entries similar to the following example.</span></span>

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
                    "message": "Request is being forwarded to the backend service.",
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
                    "message": "Response headers have been sent to the caller. Starting to stream the response body."
                }
            },
            {
                "source": "handler",
                "timestamp": "2015-06-23T19:51:35.4256650Z",
                "elapsed": "00:00:00.1963155",
                "data": {
                    "message": "Response body streaming to the caller is complete."
                }
            }
        ]
    }
}
```

## <span data-ttu-id="f1cbb-139"><a name="next-steps"> </a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f1cbb-139"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="f1cbb-140">Bekijk een demo voor tracering van beleidsexpressies in [Cloud hebben betrekking op aflevering 177: meer API Management-functies](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/).</span><span class="sxs-lookup"><span data-stu-id="f1cbb-140">Watch a demo of tracing policy expressions in [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/).</span></span> <span data-ttu-id="f1cbb-141">Vooruit tot 21:00 voor een overzicht van de demo.</span><span class="sxs-lookup"><span data-stu-id="f1cbb-141">Fast-forward to 21:00 to see the demo.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Cloud+Cover/Episode-177-More-API-Management-Features-with-Vlad-Vinogradsky/player]
> 
> 

[Use API Inspector to trace a call]: #trace-call
[Inspect the trace]: #inspect-trace
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




