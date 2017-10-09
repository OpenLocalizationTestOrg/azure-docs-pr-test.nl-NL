
<span data-ttu-id="30ad3-101">Hallo-code voor alle functies in een bepaalde functie-app Hallo woont in een hoofdmap met een configuratiebestand voor de host en een of meer submappen, die elk de Hallo-code voor een afzonderlijke functie, zoals in het volgende voorbeeld Hallo bevatten:</span><span class="sxs-lookup"><span data-stu-id="30ad3-101">hello code for all of hello functions in a given function app lives in a root folder that contains a host configuration file and one or more subfolders, each of which contain hello code for a separate function, as in hello following example:</span></span>

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

<span data-ttu-id="30ad3-102">Hallo *host.json* bestand bevat een runtime-specifieke configuratie en bevindt zich in de hoofdmap Hallo van Hallo functie-app.</span><span class="sxs-lookup"><span data-stu-id="30ad3-102">hello *host.json* file contains some runtime-specific configuration and sits in hello root folder of hello function app.</span></span> <span data-ttu-id="30ad3-103">Zie voor informatie over de instellingen die beschikbaar zijn, [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) in Hallo WebJobs.Script opslagplaats wiki.</span><span class="sxs-lookup"><span data-stu-id="30ad3-103">For information on settings that are available, see [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) in hello WebJobs.Script repository wiki.</span></span>

<span data-ttu-id="30ad3-104">Elke functie heeft een map met een of meer codebestanden, Hallo function.json configuratie en andere afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="30ad3-104">Each function has a folder that contains one or more code files, hello function.json configuration and other dependencies.</span></span>

