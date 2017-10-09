<span data-ttu-id="6cf9c-101">Verzameling van aangepaste metingen.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-101">Collection of custom measurements.</span></span> <span data-ttu-id="6cf9c-102">Deze verzameling tooreport meting Hallo telemetrie-item is gekoppeld met de naam gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-102">Use this collection tooreport named measurement associated with hello telemetry item.</span></span> <span data-ttu-id="6cf9c-103">Er zijn typische gebruiksvoorbeelden:</span><span class="sxs-lookup"><span data-stu-id="6cf9c-103">Typical use cases are:</span></span>
- <span data-ttu-id="6cf9c-104">Hallo-grootte van Afhankelijkheidstelemetrie nettolading</span><span class="sxs-lookup"><span data-stu-id="6cf9c-104">hello size of Dependency Telemetry payload</span></span>
- <span data-ttu-id="6cf9c-105">Hallo aantal wachtrij-items die zijn verwerkt door telemetrie aanvragen</span><span class="sxs-lookup"><span data-stu-id="6cf9c-105">hello number of queue items processed by Request Telemetry</span></span>
- <span data-ttu-id="6cf9c-106">tijd die klant duurde toocomplete Hallo stap in de wizard stap voltooiing gebeurtenis telemetrie.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-106">time that customer took toocomplete hello step in wizard step completion Event Telemetry.</span></span>

<span data-ttu-id="6cf9c-107">U kunt een query [aangepaste metingen](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA2WLOw6DMAyGd07hZoLeoRPqyMaGGAL8aiPhGCV2kKoeHsHK%2Bj1myyr8LoiaqfrT%2FkUCzRft4LMl8OUeL3LuLLIx%2BxR%2BIF8%2BtcoiNq2o78vgWuFthQaJ1AeGGxt6UlBwKxa1qQ6EpLhAfQAAAA%3D%3D&timespan=PT24H) in analytische gegevens van toepassing:</span><span class="sxs-lookup"><span data-stu-id="6cf9c-107">You can query [custom measurements](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA2WLOw6DMAyGd07hZoLeoRPqyMaGGAL8aiPhGCV2kKoeHsHK%2Bj1myyr8LoiaqfrT%2FkUCzRft4LMl8OUeL3LuLLIx%2BxR%2BIF8%2BtcoiNq2o78vgWuFthQaJ1AeGGxt6UlBwKxa1qQ6EpLhAfQAAAA%3D%3D&timespan=PT24H) in Application Analytics:</span></span>

```
customEvents
| where customMeasurements != ""
| summarize avg(todouble(customMeasurements["Completion Time"]) * itemCount)
```

 > [!NOTE]
 > <span data-ttu-id="6cf9c-108">Aangepaste metingen zijn gekoppeld aan Hallo telemetrie-item waartoe ze behoren.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-108">Custom measurements are associated with hello telemetry item they belong to.</span></span> <span data-ttu-id="6cf9c-109">Ze zijn onderwerp toosampling met Hallo telemetrie-item dat u deze metingen bevat.</span><span class="sxs-lookup"><span data-stu-id="6cf9c-109">They are subject toosampling with hello telemetry item containing those measurements.</span></span> <span data-ttu-id="6cf9c-110">een meting met een waarde die onafhankelijk van andere typen telemetrie, gebruik tootrack [metrische telemetrie](../articles/application-insights/app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="6cf9c-110">tootrack a measurement that has a value independent from other telemetry types, use [Metric telemetry](../articles/application-insights/app-insights-api-custom-events-metrics.md).</span></span>

<span data-ttu-id="6cf9c-111">De maximale lengte: 150</span><span class="sxs-lookup"><span data-stu-id="6cf9c-111">Max key length: 150</span></span>
