In deze stap maakt u Hallo beschikbaarheidsgroep-listener testen met behulp van een clienttoepassing die wordt uitgevoerd op Hallo hetzelfde netwerk.

Clientconnectiviteit heeft Hallo volgens de vereisten:

* Client-verbindingen toohello listener moet afkomstig zijn van de machines die zich in een andere cloudservice dan Hallo een dat hosts Hallo altijd op de beschikbaarheidsreplica's bevinden.
* Als zich in verschillende subnetten bevinden Hallo altijd op de replica's, moeten clients opgeven *MultisubnetFailover = True* in Hallo-verbindingsreeks. Dit resulteert in parallelle verbinding probeert tooreplicas in Hallo verschillende subnetten. Dit scenario bevat een regio-overschrijdende altijd op beschikbaarheid groep-implementatie.

Een voorbeeld hiervan is tooconnect toohello listener uit een Hallo virtuele machines in Hallo hetzelfde virtuele Azure-netwerk (maar niet een die als host fungeert voor een replica). Een eenvoudige manier toocomplete deze test tootry tooconnect SQL Server Management Studio toohello beschikbaarheidsgroep-listener is. Een andere eenvoudige methode is toorun [SQLCMD.exe](https://technet.microsoft.com/library/ms162773.aspx)als volgt:

    sqlcmd -S "<ListenerName>,<EndpointPort>" -d "<DatabaseName>" -Q "select @@servername, db_name()" -l 15

> [!NOTE]
> Als Hallo EndpointPort waarde *1433*, u bent geen vereiste toospecify in Hallo-aanroep. Hallo vorige aanroep wordt ervan uitgegaan dat Hallo client-computer is lid toohello hetzelfde domein en die beller Hallo machtigingen heeft op Hallo-database met behulp van Windows-verificatie.
> 
> 

Wanneer u Hallo listener test, kunnen worden ervoor toofail via Hallo beschikbaarheid groep toomake ervoor dat clients toohello listener over failovers verbinding kunnen maken.

