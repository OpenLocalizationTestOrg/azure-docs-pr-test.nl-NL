## <a name="scenario"></a>Scenario
toobetter laten zien hoe toocreate udr's, dit document maakt gebruik van onderstaande Hallo scenario.

![BESCHRIJVING VAN AFBEELDING](./media/virtual-network-create-udr-scenario-include/figure1.png)

In dit scenario maakt u een UDR voor Hallo *Front end subnet* en een andere UDR voor Hallo *subnet voor Back-end* , zoals hieronder wordt beschreven: 

* **UDR FrontEnd**. Hallo-front-end UDR worden toegepaste toohello *FrontEnd* subnet, en bevatten één route:    
  * **RouteToBackend**. Deze route stuurt alle verkeer toohello back-end subnet toohello **FW1** virtuele machine.
* **UDR-back-end**. Hallo back-end UDR worden toegepaste toohello *back-end* subnet, en bevatten één route:    
  * **RouteToFrontend**. Deze route stuurt alle verkeer toohello front-end-subnet toohello **FW1** virtuele machine.

Hallo combinatie van deze routes zorgt ervoor dat alle verkeer dat is bestemd uit één subnet tooanother zal gerouteerde toohello **FW1** virtuele machine, die wordt gebruikt als een virtueel apparaat. U moet ook tooturn op doorsturen via IP voor die VM, tooensure kan het verkeer ontvangen dat is bestemd tooother virtuele machines.

