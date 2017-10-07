---
title: aaaHow toouse Azure Redis-Cache met behulp van Python | Microsoft Docs
description: Aan de slag met Azure Redis-cache met behulp van Python
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: v-lincan
ms.assetid: f186202c-fdad-4398-af8c-aee91ec96ba3
ms.service: cache
ms.devlang: python
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/10/2017
ms.author: sdanie
ms.openlocfilehash: 74c03eb4ce17ff3574595fd2bb37e399d71c6eb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache-with-python"></a>Hoe toouse Azure Redis-Cache met behulp van Python
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Dit onderwerp leest u hoe tooget de slag met Azure Redis-Cache met behulp van Python.

## <a name="prerequisites"></a>Vereisten
Installeer [redis-py](https://github.com/andymccurdy/redis-py).

## <a name="create-a-redis-cache-on-azure"></a>Een Redis-cache maken op Azure
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a>Hallo-host en toegangssleutels ophalen
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="enable-hello-non-ssl-endpoint"></a>Niet-SSL-eindpunt Hallo inschakelen
Sommige Redis-clients bieden geen ondersteuning voor SSL en door standaard Hallo [niet-SSL-poort is uitgeschakeld voor nieuwe exemplaren van Azure Redis-Cache](cache-configure.md#access-ports). Op moment van schrijven van dit Hallo Hallo [redis-py](https://github.com/andymccurdy/redis-py) geen ondersteuning voor SSL. 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-non-ssl-port.md)]

## <a name="add-something-toohello-cache-and-retrieve-it"></a>Iets toevoegen toohello in de cache en dit ophalen
    >>> import redis
    >>> r = redis.StrictRedis(host='<name>.redis.cache.windows.net',
          port=6380, db=0, password='<key>', ssl=True)
    >>> r.set('foo', 'bar')
    True
    >>> r.get('foo')
    b'bar'


Vervang `<name>` door de cachenaam en `key` door uw toegangssleutel.

<!--Image references-->
[1]: ./media/cache-python-get-started/redis-cache-new-cache-menu.png
[2]: ./media/cache-python-get-started/redis-cache-cache-create.png
