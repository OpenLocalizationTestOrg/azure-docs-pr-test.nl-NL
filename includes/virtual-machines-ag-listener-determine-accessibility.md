Het is belangrijk toorealize dat er twee manieren tooconfigure een beschikbaarheidsgroep-listener in Azure zijn. Hallo manieren verschillen in het type hello Azure load balancer die u bij het maken van Hallo-listener. Hallo volgende tabel beschrijft Hallo verschillen:

| Type load balancer | Implementatie | Gebruiken wanneer: |
| --- | --- | --- |
| **Externe** |Maakt gebruik van Hallo *openbare virtuele IP-adres* van Hallo cloudservice die als host fungeert voor (Hallo virtuele machines). |U moet tooaccess Hallo-listener van externe Hallo virtueel netwerk, met inbegrip van Hallo Internet. |
| **Interne** |Maakt gebruik van een *interne load balancer* met een persoonlijk adres voor Hallo listener. |U hebt toegang tot Hallo-listener alleen via Hallo hetzelfde virtuele netwerk. Deze toegang bevat een site-naar-site VPN in hybride scenario's. |

> [!IMPORTANT]
> Voor een listener dat gebruikt Hallo cloudservice openbare VIP (externe load balancer), zo lang Hallo-client, de listener en de databases bevinden zich in dezelfde Azure-regio hello, kosten voor uitgaande wordt geen kosten. Geen gegevens geretourneerd anders via Hallo listener wordt beschouwd als uitgaande en wordt in rekening gebracht volgens de tarieven voor normale gegevensoverdracht. 
> 
> 

Een ILB kan alleen op virtuele netwerken met een regionaal bereik worden geconfigureerd. Bestaande virtuele netwerken die zijn geconfigureerd voor een affiniteitsgroep kunnen een ILB niet gebruiken. Zie voor meer informatie [interne load balancer overzicht](../articles/load-balancer/load-balancer-internal-overview.md).

