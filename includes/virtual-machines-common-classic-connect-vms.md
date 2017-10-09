

![Virtuele machines in een zelfstandige cloudservice](./media/virtual-machines-common-classic-connect-vms/CloudServiceExample.png)

Als u uw virtuele machines in een virtueel netwerk inschakelt, kunt u bepalen hoeveel cloud-services die u wilt dat toouse voor load balancing en beschikbaarheid sets. Bovendien kunt u virtuele machines van Hallo indelen op subnetten in Hallo dezelfde manier als uw on-premises netwerk en verbinding Hallo virtueel netwerk tooyour maken lokale netwerk. Hier volgt een voorbeeld:

![Virtuele machines in een virtueel netwerk](./media/virtual-machines-common-classic-connect-vms/VirtualNetworkExample.png)

Virtuele netwerken zijn Hallo aanbevolen manier tooconnect virtuele machines in Azure. Hallo aanbevolen procedure is tooconfigure elke laag van uw toepassing in een afzonderlijke cloudservice. Echter, moet u mogelijk toocombine sommige virtuele machines van verschillende toepassingslagen in Hallo cloud dezelfde service tooremain binnen Hallo maximaal 200 cloudservices per abonnement. tooreview dit en andere beperkingen, Zie [Azure-abonnement en Service-limieten, quota's en beperkingen](../articles/azure-subscription-service-limits.md).

## <a name="connect-vms-in-a-virtual-network"></a>Verbinding maken met virtuele machines in een virtueel netwerk
tooconnect virtuele machines in een virtueel netwerk:

1. Hallo Hallo virtueel netwerk maken [Azure-portal](../articles/virtual-network/virtual-networks-create-vnet-classic-pportal.md) en 'klassieke implementatie' opgeven.
2. Hallo-set van cloud-services voor uw implementatie tooreflect uw ontwerp voor beschikbaarheidssets maken en taakverdeling. In hello Azure-portal, klikt u op **Nieuw > berekenen > Cloudservice** voor elke cloudservice.

  Als u details van Hallo cloud service invullen, kies dezelfde Hallo _resourcegroep_ gebruikt met Hallo virtueel netwerk.

3. toocreate elke nieuwe virtuele machine, klikt u op **Nieuw > berekenen**, en selecteer Hallo juiste VM-installatiekopie uit Hallo **aanbevolen apps**.

  In Hallo VM **basisbeginselen** blade kiezen Hallo dezelfde _resourcegroep_ gebruikt met Hallo virtueel netwerk.

  ![Basisprincipes van VM-blade wanneer u een VNet](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_VN.png)

4. Terwijl u Hallo VM invult **instellingen**, kies de juiste Hallo _Cloudservice_ of _virtueel netwerk_ voor Hallo VM.

  Azure selecteert Hallo andere item op basis van uw selectie.

  ![Blade van de VM-instellingen wanneer u een VNet](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_VN.png)


## <a name="connect-vms-in-a-standalone-cloud-service"></a>Verbinding maken met virtuele machines in een zelfstandige cloudservice
tooconnect virtuele machines in een zelfstandige cloudservice:

1. Hallo-cloudservice maken in Hallo [Azure-portal](http://portal.azure.com). Klik op **Nieuw > berekenen > Cloudservice**. Of u kunt Hallo cloudservice voor uw implementatie maken bij het maken van uw eerste virtuele machine.
2. Wanneer u Hallo virtuele machines maakt, kiest u Hallo dezelfde resourcegroep met Hallo-cloudservice gebruikt.

  ![Een virtuele machine tooan bestaande cloudservice toevoegen](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_SA.png)

3.  Als u details van de VM Hallo invullen, kiest u Hallo-naam van cloudservice gemaakt in de eerste stap Hallo.

  ![Een cloudservice voor een virtuele machine selecteren](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_SA.png)
