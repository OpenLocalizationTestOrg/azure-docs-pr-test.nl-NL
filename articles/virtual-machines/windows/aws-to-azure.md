---
title: een AWS-VM's van Windows-tooAzure aaaMove | Microsoft Docs
description: Verplaatsen van een Amazon Web Services (AWS) EC2 Windows exemplaar tooAzure virtuele Machines met Azure PowerShell.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: cynthn
ms.openlocfilehash: f912c28d3ffe585162c3add715a1318ac3cd4643
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-windows-vm-from-amazon-web-services-aws-tooazure-using-powershell"></a>Een Windows VM verplaatsen van Amazon Web Services (AWS) tooAzure met behulp van PowerShell

Als u virtuele machines voor het hosten van uw workloads in Azure, kunt u een bestaand exemplaar van de virtuele machine met Amazon Web Services (AWS) EC2 Windows exporteren vervolgens Hallo virtuele harde schijf (VHD) tooAzure uploaden. Eenmaal Hallo die VHD is geüpload, kunt u een nieuwe virtuele machine in Azure uit Hallo VHD. 

In dit onderwerp bevat informatie over het verplaatsen van één VM van AWS tooAzure. Als u toomove virtuele machines van AWS tooAzure op grote schaal wilt, Zie [migreren van virtuele machines in Amazon Web Services (AWS) tooAzure met Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).

## <a name="prepare-hello-vm"></a>Hallo VM voorbereiden 
 
U kunt algemene en gespecialiseerde VHD's tooAzure uploaden. Elk type vereist dat u Hallo VM voorbereiden voordat u exporteert van AWS. 

- **VHD gegeneraliseerd** -een gegeneraliseerde VHD heeft al uw persoonlijke accountgegevens verwijderd met behulp van Sysprep. Als u van plan toouse Hallo VHD als een installatiekopie toocreate bent nieuwe virtuele machines van moet: 
 
    * [Voorbereiden van een Windows VM](prepare-for-upload-vhd-image.md).  
    * Generalize Hallo virtuele machine met behulp van Sysprep.  

 
- **VHD gespecialiseerde** -een gespecialiseerde VHD onderhoudt Hallo gebruikersaccounts, toepassingen en andere statusgegevens van uw oorspronkelijke VM. Als u van plan toouse bent Hallo VHD-toocreate is een nieuwe virtuele machine, Controleer Hallo stappen zijn voltooid.  
    * [Voorbereiden van een Windows-VHD tooupload tooAzure](prepare-for-upload-vhd-image.md). **Geen** generalize Hallo van virtuele machine met behulp van Sysprep. 
    * Verwijder eventuele Gast virtualisatie-hulpprogramma's en de agents die zijn geïnstalleerd op Hallo VM (dat wil zeggen VMware tools). 
    * Zorg ervoor dat Hallo VM geconfigureerde toopull is het IP-adres en DNS-instellingen via DHCP. Dit zorgt ervoor dat Hallo-server verkrijgt IP-adres binnen Hallo VNet wanneer deze opgestart wordt.  


## <a name="export-and-download-hello-vhd"></a>Exporteren en Hallo VHD downloaden 

Hallo EC2 exemplaar tooa VHD in een Amazon S3-bucket exporteren. Volg de stappen Hallo in Hallo Amazon-documentatie-onderwerp [exporteren van een exemplaar als een virtuele machine met behulp van virtuele machine importeren/exporteren](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) en Voer Hallo [-exemplaar-export-taak maken](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) opdracht tooexport Hallo EC2 exemplaar tooa VHD-bestand. 

Hallo wordt geëxporteerde VHD-bestand opgeslagen in Hallo Amazon S3-bucket die u opgeeft. Hallo basic syntaxis voor exporteren Hallo VHD lager is dan, vervangt Hallo tijdelijke aanduiding voor tekst in <brackets> met uw gegevens.

```
aws ec2 create-instance-export-task --instance-id <instanceID> --target-environment Microsoft \
  --export-to-s3-task DiskImageFormat=VHD,ContainerFormat=ova,S3Bucket=<bucket>,S3Prefix=<prefix>
```

Eenmaal Hallo VHD geëxporteerd werden, volg de instructies Hallo in [hoe kan ik een Object downloaden van een S3-Bucket?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) toodownload Hallo VHD-bestand van Hallo S3-bucket. 

> [!IMPORTANT]
> AWS brengt gegevensoverdracht kosten voor het downloaden van Hallo VHD. Zie [Amazon S3 prijzen](https://aws.amazon.com/s3/pricing/) voor meer informatie.


## <a name="next-steps"></a>Volgende stappen

U kunt nu Hallo VHD tooAzure uploaden en maken van een nieuwe virtuele machine. 

- Als u Sysprep uitgevoerd op de bron te**generalize** deze voordat u exporteert, Zie [een gegeneraliseerde VHD uploaden en toocreate een nieuwe virtuele machines in Azure gebruiken](upload-generalized-managed.md)
- Als u niet Sysprep hebt uitgevoerd voordat u exporteert, hello VHD wordt beschouwd als **gespecialiseerde**, Zie [een gespecialiseerde VHD tooAzure uploaden en een nieuwe virtuele machine maken](create-vm-specialized.md)

 
