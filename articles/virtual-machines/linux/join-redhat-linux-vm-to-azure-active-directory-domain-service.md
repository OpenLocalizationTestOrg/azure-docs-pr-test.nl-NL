---
title: een virtuele Linux-machine RedHat tooan Azure Active Directory DS aaaJoin | Microsoft Docs
description: Hoe toojoin een bestaande RedHat Enterprise Linux 7 VM tooan Azure Active Directory Domain Services.
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/14/2016
ms.author: v-livech
ms.openlocfilehash: f3ba3c764e253191753f1cc5fc8c3b85c53818af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-redhat-linux-vm-tooan-azure-active-directory-domain-service"></a>Deelnemen aan een virtuele Linux-machine RedHat tooan Azure Active Directory Domain Services

Dit artikel laat zien hoe een virtuele machine tooan voor Red Hat Enterprise Linux (RHEL) 7 Azure Active Directory Domain Services (AADDS) toojoin beheerd domein.  Hallo-vereisten zijn:

- [een Azure-account.](https://azure.microsoft.com/pricing/free-trial/)

- [bestanden voor openbare en persoonlijke SSH-sleutels](mac-create-ssh-keys.md)

- [een Azure Active Directory Domain Services-DC](../../active-directory-domain-services/active-directory-ds-getting-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a>Snelle opdrachten

_Geen voorbeelden vervangen door uw eigen instellingen._

### <a name="switch-hello-azure-cli-tooclassic-deployment-mode"></a>Hello azure-cli tooclassic implementatie-modus schakelen

```azurecli
azure config mode asm
```

### <a name="search-for-a-rhel-version-and-image"></a>Zoeken naar een RHEL-versie en een installatiekopie

```azurecli
azure vm image list | grep "Red Hat"
```

### <a name="create-a-redhat-linux-vm"></a>Een Redhat Linux VM maken

```azurecli
azure vm create myVM \
-o a879bbefc56a43abb0ce65052aac09f3__RHEL_7_2_Standard_Azure_RHUI-20161026220742 \
-g ahmet \
-p myPassword \
-e 22 \
-t "~/.ssh/id_rsa.pub" \
-z "Small" \
-l "West US"
```

### <a name="ssh-toohello-vm"></a>SSH toohello VM

```bash
ssh -i ~/.ssh/id_rsa ahmet@myVM
```

### <a name="update-yum-packages"></a>YUM pakketten bijwerken

```bash
sudo yum update
```

### <a name="install-packages-needed"></a>Installeren van pakketten nodig

```bash
sudo yum -y install realmd sssd krb5-workstation krb5-libs
```

Nu vereist hello-pakketten op Hallo virtuele Linux-machine zijn geïnstalleerd, de volgende taak Hallo is toojoin Hallo virtuele machine toohello beheerd domein.

### <a name="discover-hello-aad-domain-services-managed-domain"></a>Hallo AAD Domain Services beheerd domein detecteren

```bash
sudo realm discover mydomain.com
```

### <a name="initialize-kerberos"></a>Initialiseren van kerberos

Zorg ervoor dat u opgeeft dat een gebruiker die lid is van toohello ' AAD DC' beheerdersgroep. Alleen deze gebruikers kunnen computers toohello beheerd domein toevoegen.

```bash
kinit ahmet@mydomain.com
```

### <a name="join-hello-machine-toohello-domain"></a>Lid worden van Hallo machine toohello domein

```bash
sudo realm join --verbose mydomain.com -U 'ahmet@mydomain.com'
```

### <a name="verify-hello-machine-is-joined-toohello-domain"></a>Controleer of de machine Hallo gekoppelde toohello domein

```bash
ssh -l ahmet@mydomain.com mydomain.cloudapp.net
```

## <a name="next-steps"></a>Volgende stappen

* [Red Hat Update-infrastructuur (RHUI) voor on-demand Red Hat Enterprise Linux virtuele machines in Azure](update-infrastructure-redhat.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Sleutelkluis instellen voor virtuele machines in Azure Resource Manager](key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Implementeren en beheren van virtuele machines met behulp van Azure Resource Manager-sjablonen en hello Azure CLI](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
