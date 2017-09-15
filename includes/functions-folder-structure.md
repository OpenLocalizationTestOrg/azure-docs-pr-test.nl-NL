
<span data-ttu-id="a5d40-101">De code voor alle functies in een bepaalde functie-app woont in een hoofdmap met een configuratiebestand van de host en een of meer submappen, elk waarvan de code voor een afzonderlijke functie, zoals in het volgende voorbeeld bevat:</span><span class="sxs-lookup"><span data-stu-id="a5d40-101">The code for all of the functions in a given function app lives in a root folder that contains a host configuration file and one or more subfolders, each of which contain the code for a separate function, as in the following example:</span></span>

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

<span data-ttu-id="a5d40-102">De *host.json* bestand bevat een runtime-specifieke configuratie en bevindt zich in de hoofdmap van de functie-app.</span><span class="sxs-lookup"><span data-stu-id="a5d40-102">The *host.json* file contains some runtime-specific configuration and sits in the root folder of the function app.</span></span> <span data-ttu-id="a5d40-103">Zie voor informatie over de instellingen die beschikbaar zijn, [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) in de opslagplaats WebJobs.Script wiki.</span><span class="sxs-lookup"><span data-stu-id="a5d40-103">For information on settings that are available, see [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) in the WebJobs.Script repository wiki.</span></span>

<span data-ttu-id="a5d40-104">Elke functie heeft een map met een of meer codebestanden, de configuratie van de function.json en andere afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="a5d40-104">Each function has a folder that contains one or more code files, the function.json configuration and other dependencies.</span></span>

