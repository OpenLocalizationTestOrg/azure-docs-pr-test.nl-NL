# <a name="securing-docker-containers-in-azure-container-service"></a>Docker-containers beveiligen in Azure Container Service

Dit artikel bevat overwegingen en aanbevelingen voor het beveiligen van Docker-containers die zijn geïmplementeerd in Azure Container Service. Veel van deze overwegingen van toepassing in het algemeen tooDocker containers die zijn geïmplementeerd in Azure of andere omgevingen. 

## <a name="image-security"></a>Beveiliging van installatiekopieën

Containers worden gemaakt van installatiekopieën die zijn opgeslagen in een of meer opslagplaatsen. Deze opslagplaatsen kunnen toopublic of privé-container registers behoren. Een voorbeeld van een openbaar register is [Docker Hub](https://hub.docker.com/). Een voorbeeld van een persoonlijke register is Hallo [Docker vertrouwde register](https://docs.docker.com/datacenter/dtr/2.0/), die kan worden geïnstalleerd op de lokale of in een virtuele privécloud. Er zijn ook cloudgebaseerde persoonlijke containerregisterservices, waaronder [Azure Container Registry](../articles/container-registry/container-registry-intro.md).

### <a name="public-and-private-images"></a>Openbare en persoonlijke installatiekopieën
In het algemeen kan voor een openbaar beschikbare containerinstallatiekopie geen veiligheid worden gegarandeerd, net als bij elk openbaar gepubliceerd softwarepakket. Containerinstallatiekopieën bestaan uit meerdere softwarelagen en elke softwarelaag kan beveiligingsproblemen bevatten. Het belangrijkste toounderstand Hallo oorsprong van Hallo container afbeelding is, inclusief Hallo eigenaar van Hallo-afbeelding (toodetermine als het een betrouwbare bron of niet), Hallo softwarelagen bestaat uit en Hallo softwareversies. 

Bijvoorbeeld, als u toohello officiële gaan [nginx-opslagplaats](https://hub.docker.com/_/nginx/) in Docker-Hub en navigeer toohello **labels** tabblad ziet u gekleurde beveiligingslekken in elke installatiekopie. Elke kleur beschrijft Hallo kwetsbaarheid van een softwarelaag van Hallo-afbeelding. Zie [Understanding official repos on Docker Hub](https://blog.docker.com/2015/06/understanding-official-repos-docker-hub/) (Officiële opslagplaatsen in Docker Hub begrijpen) voor meer informatie over het scannen van beveiligingsproblemen in Docker Hub.

![Nginx-afbeeldingen in Docker Hub](./media/container-service-security/docker-hub-nginx.png)

Ondernemingen care diep over beveiligings- en tooprotect moeten zichzelf tegen een aanval op de beveiliging opslaan en ophalen van installatiekopieën van een persoonlijke register, zoals Azure Container register of vertrouwde Docker-register. In aanvulling tooproviding een beheerde persoonlijke register, Azure Container register ondersteunt [service-principal gebaseerde verificatie](../articles/container-registry/container-registry-authentication.md) via Azure Active Directory voor basisverificatie stromen, met inbegrip van toegang op basis van rollen voor alleen-lezen, schrijven en van eigenaarsmachtigingen.

### <a name="image-security-scanning"></a>Installatiekopieën scannen op veiligheid

Zelfs wanneer u een persoonlijke register, is een goed idee toouse installatiekopie van het scannen van oplossingen voor aanvullende beveiligingsverificatie. Elke laag software in een installatiekopie van een container is mogelijk kwetsbaar toovulnerabilities onafhankelijk van andere lagen in Hallo container afbeelding. Steeds meer bedrijven gestart hun productieworkloads op basis van de container technologieën implementeren, wordt het scannen van afbeeldingen belangrijk tooensure preventie van bedreigingen van hun organisatie. 

Beveiliging bewaken en scannen oplossingen zoals [Twistlock](https://www.twistlock.com/2016/11/07/twistlock-supports-azure-container-registry) en [zeeblauw beveiliging](http://blog.aquasec.com/image-vulnerability-scanning-in-azure-container-registry), onder andere kunnen worden gebruikt tooscan container afbeeldingen in een persoonlijke register en mogelijke beveiligingsproblemen te identificeren. Het is belangrijk toounderstand Hallo diepte van scannen die verschillende Hallo-oplossingen bieden. Bepaalde oplossingen controleren de lagen van de installatiekopie bijvoorbeeld alleen maar op bekende beveiligingsproblemen. Deze oplossingen mogelijk niet kunnen tooverify installatiekopie laag software die via bepaalde manager-software van het pakket is gemaakt. Andere oplossingen hebben diepere scanintegratie en kunnen beveiligingsproblemen in alle verpakte software vinden.

### <a name="production-deployment-rules-and-audit"></a>Regels voor productie-implementatie en controle
Zodra een toepassing is geïmplementeerd in productie, is het essentieel tooset een paar regels tooensure waarmee afbeeldingen in productieomgevingen zijn beveiligd en bevatten geen beveiligingsproblemen.

* Als een regel afbeeldingen met beveiligingsproblemen, zelfs secundaire mogen niet toorun in een productieomgeving. Bovendien moeten alle installatiekopieën die zijn geïmplementeerd in de productieomgeving in het ideale geval worden opgeslagen in een persoonlijke register toegankelijk tooa select weinig. Het is ook belangrijk tookeep Hallo aantal productie installatiekopieën kleine tooensure dat deze effectief kunnen worden beheerd.

* Omdat het vaste toopinpoint Hallo oorsprong van software van een installatiekopie van een container openbaar beschikbaar is, is een goede gewoonte toobuild installatiekopieën van de bron tooensure kennis van de oorsprong Hallo van Hallo laag. Wanneer een vlakken beveiligingslek in een installatiekopie zelf ingebouwde container, kunnen klanten een sneller pad tooa-oplossing te vinden. Met een openbare-installatiekopie klanten toofind Hallo hoofdmap van een installatiekopie van het openbare-toofix moet deze of een andere veilige installatiekopie verkrijgen van Hallo uitgever.

* Een grondig gescande afbeelding geïmplementeerd in productie is niet toobe up toodate voor Hallo levensduur van de toepassing hello gegarandeerd. Beveiligingsproblemen mogelijk worden gerapporteerd voor de lagen van de afbeelding Hallo die niet eerder bekend of na Hallo productie-implementatie zijn geïntroduceerd. Periodieke controle van installatiekopieën die zijn geïmplementeerd in productie is noodzakelijk tooidentify afbeeldingen die zijn verouderd of in een tijdje niet zijn bijgewerkt. Een implementatie van blauw groen methoden en rolling upgrade mechanismen tooupdate container installatiekopieën zonder uitvaltijd mogelijk gebruiken. Scannen van afbeeldingen kan worden gedaan met hulpprogramma's beschreven in voorgaande sectie Hallo. 

* Een pijplijn continue integratie (CI) toobuild installatiekopieën en het scannen van geïntegreerde beveiliging kunt onderhouden van veilige persoonlijke registers met beveiligde container-installatiekopieën. Hallo beveiligingslek scannen ingebouwd in Hallo CI oplossing zorgt ervoor dat de installatiekopieën die slagen voor alle tests van Hallo toohello persoonlijke register uit welke productie werkbelastingen zijn geïmplementeerd zijn geactiveerd. Een CI-pipeline-fout zorgt ervoor dat kwetsbaar afbeeldingen niet worden geactiveerd in Hallo persoonlijke register gebruikt voor productie-implementaties van werkbelasting. Met de pijplijn kunt u ook beveiligingsscans voor de installatiekopieën automatisch laten uitvoeren bij een groot aantal installatiekopieën. Het handmatig controleren van installatiekopieën op beveiligingsproblemen kan erg langdurig en foutgevoelig zijn.

## <a name="host-level-container-isolation"></a>Isolatie van containers op hostniveau
Wanneer een klant containertoepassingen op Azure-resources implementeert, worden ze op een abonnementsniveau in resourcegroepen geïmplementeerd en hebben ze niet meerdere tenants. Dit betekent dat als een klant een abonnement met anderen deelt, er zijn geen grenzen die kunnen worden opgebouwd tussen twee implementaties in Hallo hetzelfde abonnement. Beveiliging op containerniveau kan daarom niet worden gegarandeerd. 

Het is ook kritieke toounderstand dat containers delen Hallo kernel en Hallo bronnen van het Hallo-host (die in Azure Container Service is een Azure-virtuele machine in een cluster). Containers die worden uitgevoerd in de productieomgeving moeten daarom worden uitgevoerd in de modus voor niet-gemachtigde gebruikers. Een container met basis-bevoegdheden uitgevoerd kan Hallo gehele omgeving in gevaar brengen. Met toegang op hoofdniveau in een container, kan een hacker toegang krijgen toohello volledige hoofdmap bevoegdheden op Hallo host. Bovendien is het belangrijk toorun containers met alleen-lezen-bestandssystemen. Dit voorkomt dat iemand die toegang toohello geknoeid container toowrite schadelijke scripts toohello bestandssysteem en toegang krijgen tot bestanden tooother heeft. Daarnaast is het belangrijk toolimit Hallo bronnen (zoals geheugen, CPU en netwerkbandbreedte), tooa container toegewezen. Dit helpt voorkomen dat hackers vasthouden van resources en kunt u onwettige activiteiten zoals fraude of bitcoin mijnbouw, die kan voorkomen dat andere containers op Hallo host of cluster wordt uitgevoerd.

## <a name="orchestrator-considerations"></a>Orchestratoroverwegingen

Elke orchestrator die beschikbaar is in Azure Container Service heeft zijn eigen beveiligingsoverwegingen. Bijvoorbeeld, kunt u direct SSH toegang tooorchestrator knooppunten in de Container Service beperken. In plaats daarvan moet u de gebruikersinterface of de opdrachtregelprogramma's voor elke orchestrator (zoals `kubectl` voor Kubernetes) toomanage Hallo container omgeving zonder toegang tot Hallo-hosts. Zie voor meer informatie [maken van een verbinding met extern tooa Kubernetes, DC/OS of Docker Swarm-cluster](../articles/container-service/kubernetes/container-service-connect.md).

Zie voor extra beveiliging van de orchestrator-specifieke informatie Hallo resources te volgen:

* **Kubernetes**: [aanbevolen beveiligingsprocedures voor Kubernetes-implementatie](http://blog.kubernetes.io/2016/08/security-best-practices-kubernetes-deployment.html)

* **DC/OS**: [uw Cluster beveiligen](https://dcos.io/docs/1.8/administration/securing-your-cluster/)

* **Docker Swarm**: [Docker-beveiliging](https://www.docker.com/docker-security)

## <a name="next-steps"></a>Volgende stappen

* Zie voor meer informatie over Docker-architectuur en container beveiliging [inleiding tooContainer beveiliging](https://www.docker.com/sites/default/files/WP_IntrotoContainerSecurity_08.19.2016.pdf).

* Zie voor informatie over de beveiliging van de Azure-platform Hallo [Azure Security Center](https://www.microsoft.com/en-us/trustcenter/cloudservices/azure).
