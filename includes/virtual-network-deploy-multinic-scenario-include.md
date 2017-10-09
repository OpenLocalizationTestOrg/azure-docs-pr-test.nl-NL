## <a name="scenario"></a>Scenario
Dit document begeleidt bij een implementatie met meerdere NIC's in virtuele machines in een specifiek scenario. In dit scenario hebt u een IaaS twee lagen werkbelasting gehost in Azure. Elke laag wordt geïmplementeerd in een eigen subnet in een virtueel netwerk (VNet). Hallo-front-endlaag bestaat uit verschillende webservers, gegroepeerd in een load balancer ingesteld voor hoge beschikbaarheid. Hallo back-endlaag bestaat uit meerdere databaseservers. Deze databaseservers met twee NIC's, één voor toegang tot de database wordt geïmplementeerd, andere Hallo voor beheer. Hallo scenario omvat ook Netwerkbeveiligingsgroepen (nsg's) toocontrol welk verkeer is toegestaan tooeach subnet en NIC in Hallo-implementatie. Hallo afbeelding hieronder toont de basisarchitectuur Hallo van dit scenario.  

![MultiNIC scenario](./media/virtual-network-deploy-multinic-scenario-include/Figure1.png)

