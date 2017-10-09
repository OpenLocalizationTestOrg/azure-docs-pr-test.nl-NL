Verzameling van aangepaste metingen. Deze verzameling tooreport meting Hallo telemetrie-item is gekoppeld met de naam gebruiken. Er zijn typische gebruiksvoorbeelden:
- Hallo-grootte van Afhankelijkheidstelemetrie nettolading
- Hallo aantal wachtrij-items die zijn verwerkt door telemetrie aanvragen
- tijd die klant duurde toocomplete Hallo stap in de wizard stap voltooiing gebeurtenis telemetrie.

U kunt een query [aangepaste metingen](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA2WLOw6DMAyGd07hZoLeoRPqyMaGGAL8aiPhGCV2kKoeHsHK%2Bj1myyr8LoiaqfrT%2FkUCzRft4LMl8OUeL3LuLLIx%2BxR%2BIF8%2BtcoiNq2o78vgWuFthQaJ1AeGGxt6UlBwKxa1qQ6EpLhAfQAAAA%3D%3D&timespan=PT24H) in analytische gegevens van toepassing:

```
customEvents
| where customMeasurements != ""
| summarize avg(todouble(customMeasurements["Completion Time"]) * itemCount)
```

 > [!NOTE]
 > Aangepaste metingen zijn gekoppeld aan Hallo telemetrie-item waartoe ze behoren. Ze zijn onderwerp toosampling met Hallo telemetrie-item dat u deze metingen bevat. een meting met een waarde die onafhankelijk van andere typen telemetrie, gebruik tootrack [metrische telemetrie](../articles/application-insights/app-insights-api-custom-events-metrics.md).

De maximale lengte: 150
