Er zijn enkele beperkingen op Hallo aantal metrische gegevens en gebeurtenissen per toepassing (dat wil zeggen, per instrumentatiesleutel). Limieten, is afhankelijk van Hallo [prijzen plan](https://azure.microsoft.com/pricing/details/application-insights/) die u kiest.

| **Resource** | **Standaardlimiet** | **Opmerking**
| --- | --- | --- |
| Totale hoeveelheid gegevens per dag | 500 GB | U kunt gegevens beperken door een maximum in te stellen. Als u meer nodig hebt, kunt u een e-mail sturen naar AIDataCap@microsoft.com.
| Gratis gegevens per maand<br/> (prijscategorie Basic) | 1 GB | Aanvullende gegevens worden per gigabyte in rekening gebracht.
| Beperking | 32.000 gebeurtenissen per seconde | Hallo-limiet wordt gemeten in een minuut.
| Bewaartijd van gegevens | 90 dagen | Deze resource is voor [Search](../articles/application-insights/app-insights-diagnostic-search.md), [Analytics](../articles/application-insights/app-insights-analytics.md) en [Metrics Explorer](../articles/application-insights/app-insights-metrics-explorer.md).
| Bewaartijd van gedetailleerde resultaten van [beschikbaarheidstests met meerdere stappen](../articles/application-insights/app-insights-monitor-web-app-availability.md#multi-step-web-tests) | 90 dagen | Deze resource biedt gedetailleerde resultaten van elke stap.
| Maximale gebeurtenisgrootte | 64 KB | 
| Naamlengte voor de eigenschappen en meetgegevens | 150 | Zie [typt u schema's](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/EndpointSpecs/Schemas/Docs/)
| Lengte van de tekenreeks eigenschapswaarde | 8.192 | Zie [typt u schema's](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/EndpointSpecs/Schemas/Docs/)
| Lengte van berichten voor tracering en uitzonderingen | 10.000 | Zie [typt u schema's](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/EndpointSpecs/Schemas/Docs/)
| Aantal [beschikbaarheidstests](../articles/application-insights/app-insights-monitor-web-app-availability.md) per app  | 10 |
| [Profiler](../articles/application-insights/app-insights-profiler.md) bewaren van gegevens | Er zijn vijf dagen |
| [Profiler](../articles/application-insights/app-insights-profiler.md) gegevens verzonden per dag | 10GB |

Zie [Over prijzen en quota voor Application Insights](../articles/application-insights/app-insights-pricing.md) voor meer informatie.

