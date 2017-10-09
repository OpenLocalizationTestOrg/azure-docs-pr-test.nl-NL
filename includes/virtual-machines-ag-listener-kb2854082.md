Als alle servers op Hallo cluster werkt met Windows Server 2008 R2 of Windows Server 2012, moet u vervolgens deze hotfix Hallo controleren [KB2854082](http://support.microsoft.com/kb/2854082) is geïnstalleerd op elke Hallo lokale servers of virtuele Azure-machines die deel van het Hallo-cluster uitmaken. Een server of de virtuele machine die in Hallo-cluster, maar niet in de beschikbaarheidsgroep hello, moet u ook deze hotfix is geïnstalleerd hebben.

Hallo extern bureaublad-sessiehost voor elk van de clusterknooppunten hello, downloaden [KB2854082](http://support.microsoft.com/kb/2854082) tooa lokale map. Vervolgens installeert u Hallo hotfix op elk clusterknooppunt sequentieel worden verwerkt. Als Hallo cluster-service wordt momenteel uitgevoerd op het clusterknooppunt Hallo, opnieuw aan Hallo einde van de installatie van de hotfix Hallo Hallo server gestart.

> [!WARNING]
> Hallo-clusterservice stoppen of het Hallo-server opnieuw wordt opgestart is van invloed op Hallo quorum status van uw cluster en het Hallo-beschikbaarheidsgroep en kan ertoe leiden dat uw cluster toogo offline. toomaintain hello hoge beschikbaarheid van uw cluster tijdens de installatie, zorg ervoor dat:
> 
> * Hallo-cluster is in de status van de optimale quorum. 
> * Voordat u Hallo hotfix op een willekeurig knooppunt installeert, zijn alle clusterknooppunten online.
> * Voordat u Hallo hotfix op elk knooppunt in het Hallo-cluster installeert, kunt u Hallo hotfix installatie toorun toocompletion op één knooppunt, met inbegrip van Hallo-server volledig opnieuw te starten.
> 
> 

