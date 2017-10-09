Azure Load Balancer is een Layer-4 (TCP, UDP) load balancer. Hallo load balancer biedt hoge beschikbaarheid door het distribueren van inkomend verkeer tussen orde service-exemplaren in cloudservices of virtuele machines in een load balancer-set. Azure Load Balancer kan deze services ook toepassen op meerdere poorten, meerdere IP-adressen of allebei.

U kunt een load balancer configureren voor:

* Saldo binnenkomende Internet verkeer toovirtual machines (VM's) worden geladen. We verwijzen tooa load balancer in dit scenario als een [Internet gerichte load balancer](../articles/load-balancer/load-balancer-internet-overview.md).
* Taakverdeling voor verkeer tussen VM's in een virtueel netwerk (VNet), tussen VM's in cloudservices of tussen on-premises computers en VM's in een cross-premises virtueel netwerk. We verwijzen tooa load balancer in dit scenario als een [interne load balancer (ILB)](../articles/load-balancer/load-balancer-internal-overview.md).
* Doorsturen externe verkeer tooa specifieke VM-instantie.
