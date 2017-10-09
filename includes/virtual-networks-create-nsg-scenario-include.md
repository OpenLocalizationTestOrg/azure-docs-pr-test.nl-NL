## <a name="scenario"></a>Scenario
toobetter laten zien hoe toocreate NSGs, dit document maakt gebruik van onderstaande Hallo scenario.

![VNet-scenario](./media/virtual-networks-create-nsg-scenario-include/figure1.png)

In dit scenario maakt u een NSG voor elk subnet in Hallo **TestVNet** virtueel netwerk, zoals hieronder beschreven: 

* **NSG-FrontEnd**. Hallo-front-end NSG worden toegepaste toohello *FrontEnd* subnet, en bevatten twee regels:    
  * **RDP-regel**. Deze regel kan de RDP-verkeer toohello *FrontEnd* subnet.
  * **Web-regel**. Deze regel kunnen HTTP-verkeer toohello *FrontEnd* subnet.
* **NSG-back-end**. Hallo back-end NSG wordt toegepast toohello worden *back-end* subnet, en bevatten twee regels:    
  * **SQL-regel**. Met deze regel kunnen SQL verkeer alleen via Hallo *FrontEnd* subnet.
  * **Web-regel**. Deze regel niet alle verkeer van Hallo gebonden *back-end* subnet.

Hallo combinatie van deze regels maken van een DMZ-achtige scenario, waarbij Hallo back-end-subnet kan alleen binnenkomende verkeer voor SQL van de front-end-subnet Hallo ontvangen en heeft geen toohello toegang tot Internet, terwijl de front-end-subnet Hallo met de Hallo Internet communiceren kan, en binnenkomende HTTP-aanvragen ontvangen.

