
Hallo-code voor alle functies in een bepaalde functie-app Hallo woont in een hoofdmap met een configuratiebestand voor de host en een of meer submappen, die elk de Hallo-code voor een afzonderlijke functie, zoals in het volgende voorbeeld Hallo bevatten:

```
wwwroot
 | - host.json
 | - mynodefunction
 | | - function.json
 | | - index.js
 | | - node_modules
 | | | - ... packages ...
 | | - package.json
 | - mycsharpfunction
 | | - function.json
 | | - run.csx
```

Hallo *host.json* bestand bevat een runtime-specifieke configuratie en bevindt zich in de hoofdmap Hallo van Hallo functie-app. Zie voor informatie over de instellingen die beschikbaar zijn, [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) in Hallo WebJobs.Script opslagplaats wiki.

Elke functie heeft een map met een of meer codebestanden, Hallo function.json configuratie en andere afhankelijkheden.

