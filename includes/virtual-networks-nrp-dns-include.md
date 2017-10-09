## <a name="azure-dns"></a><span data-ttu-id="a37e1-101">Azure DNS</span><span class="sxs-lookup"><span data-stu-id="a37e1-101">Azure DNS</span></span>
<span data-ttu-id="a37e1-102">Azure DNS is een hosting service voor DNS-domeinen omzetten van namen met behulp van Microsoft Azure-infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="a37e1-102">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span></span>

| <span data-ttu-id="a37e1-103">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="a37e1-103">Property</span></span> | <span data-ttu-id="a37e1-104">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a37e1-104">Description</span></span> | <span data-ttu-id="a37e1-105">Voorbeeldwaarde</span><span class="sxs-lookup"><span data-stu-id="a37e1-105">Sample Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a37e1-106">**DNSzones**</span><span class="sxs-lookup"><span data-stu-id="a37e1-106">**DNSzones**</span></span> |<span data-ttu-id="a37e1-107">Domein zone informatie toohost DNS-records van een bepaald domein</span><span class="sxs-lookup"><span data-stu-id="a37e1-107">Domain zone information toohost DNS records of a particular domain</span></span> |<span data-ttu-id="a37e1-108">/ subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com '</span><span class="sxs-lookup"><span data-stu-id="a37e1-108">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com"</span></span> |

### <a name="dns-record-sets"></a><span data-ttu-id="a37e1-109">DNS-recordsets</span><span class="sxs-lookup"><span data-stu-id="a37e1-109">DNS record sets</span></span>
<span data-ttu-id="a37e1-110">DNS-zones hebben een onderliggend object met de naam Recordset.</span><span class="sxs-lookup"><span data-stu-id="a37e1-110">DNS zones have a child object named record set.</span></span> <span data-ttu-id="a37e1-111">Recordsets zijn een verzameling van hostrecords per voor een DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="a37e1-111">Record sets are a collection of host records by type for a DNS zone.</span></span> <span data-ttu-id="a37e1-112">Recordtypen worden A, AAAA, CNAME, MX, NS, SOA, SRV en TXT.</span><span class="sxs-lookup"><span data-stu-id="a37e1-112">Record types are A, AAAA, CNAME, MX, NS, SOA,SRV and TXT.</span></span>

| <span data-ttu-id="a37e1-113">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="a37e1-113">Property</span></span> | <span data-ttu-id="a37e1-114">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a37e1-114">Description</span></span> | <span data-ttu-id="a37e1-115">Voorbeeldwaarde</span><span class="sxs-lookup"><span data-stu-id="a37e1-115">Sample value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a37e1-116">A</span><span class="sxs-lookup"><span data-stu-id="a37e1-116">A</span></span> |<span data-ttu-id="a37e1-117">IPv4-recordtype</span><span class="sxs-lookup"><span data-stu-id="a37e1-117">IPv4 record type</span></span> |<span data-ttu-id="a37e1-118">/Subscriptions/{GUID}/.../providers/Microsoft.Network/dnszones/contoso.com/A/www</span><span class="sxs-lookup"><span data-stu-id="a37e1-118">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/A/www</span></span> |
| <span data-ttu-id="a37e1-119">AAAA</span><span class="sxs-lookup"><span data-stu-id="a37e1-119">AAAA</span></span> |<span data-ttu-id="a37e1-120">IPv6-recordtype</span><span class="sxs-lookup"><span data-stu-id="a37e1-120">IPv6 record type</span></span> |<span data-ttu-id="a37e1-121">/Subscriptions/{GUID}/.../providers/Microsoft.Network/dnszones/contoso.com/AAAA/hostrecord</span><span class="sxs-lookup"><span data-stu-id="a37e1-121">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/AAAA/hostrecord</span></span> |
| <span data-ttu-id="a37e1-122">CNAME</span><span class="sxs-lookup"><span data-stu-id="a37e1-122">CNAME</span></span> |<span data-ttu-id="a37e1-123">canonieke naam recordtype <sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="a37e1-123">canonical name record type <sup>1</sup></span></span> |<span data-ttu-id="a37e1-124">/Subscriptions/{GUID}/.../providers/Microsoft.Network/dnszones/contoso.com/CNAME/www</span><span class="sxs-lookup"><span data-stu-id="a37e1-124">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/CNAME/www</span></span> |
| <span data-ttu-id="a37e1-125">MX</span><span class="sxs-lookup"><span data-stu-id="a37e1-125">MX</span></span> |<span data-ttu-id="a37e1-126">e-recordtype</span><span class="sxs-lookup"><span data-stu-id="a37e1-126">mail record type</span></span> |<span data-ttu-id="a37e1-127">/Subscriptions/{GUID}/.../providers/Microsoft.Network/dnszones/contoso.com/MX/mail</span><span class="sxs-lookup"><span data-stu-id="a37e1-127">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/MX/mail</span></span> |
| <span data-ttu-id="a37e1-128">NS</span><span class="sxs-lookup"><span data-stu-id="a37e1-128">NS</span></span> |<span data-ttu-id="a37e1-129">naam server recordtype</span><span class="sxs-lookup"><span data-stu-id="a37e1-129">name server record type</span></span> |<span data-ttu-id="a37e1-130">/Subscriptions/{GUID}/.../providers/Microsoft.Network/dnszones/contoso.com/NS/</span><span class="sxs-lookup"><span data-stu-id="a37e1-130">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/NS/</span></span> |
| <span data-ttu-id="a37e1-131">SOA</span><span class="sxs-lookup"><span data-stu-id="a37e1-131">SOA</span></span> |<span data-ttu-id="a37e1-132">Begin van het recordtype autoriteit <sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="a37e1-132">Start of Authority record type <sup>2</sup></span></span> |<span data-ttu-id="a37e1-133">/Subscriptions/{GUID}/.../providers/Microsoft.Network/dnszones/contoso.com/SOA</span><span class="sxs-lookup"><span data-stu-id="a37e1-133">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SOA</span></span> |
| <span data-ttu-id="a37e1-134">SRV</span><span class="sxs-lookup"><span data-stu-id="a37e1-134">SRV</span></span> |<span data-ttu-id="a37e1-135">recordtype Service</span><span class="sxs-lookup"><span data-stu-id="a37e1-135">service record type</span></span> |<span data-ttu-id="a37e1-136">/Subscriptions/{GUID}/.../providers/Microsoft.Network/dnszones/contoso.com/SRV</span><span class="sxs-lookup"><span data-stu-id="a37e1-136">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SRV</span></span> |

<span data-ttu-id="a37e1-137"><sup>1</sup> staat slechts één waarde per Recordset.</span><span class="sxs-lookup"><span data-stu-id="a37e1-137"><sup>1</sup> only allows one value per record set.</span></span>

<span data-ttu-id="a37e1-138"><sup>2</sup> staat slechts één recordtype SOA per DNS-zone.</span><span class="sxs-lookup"><span data-stu-id="a37e1-138"><sup>2</sup> only allows one record type SOA per DNS zone.</span></span> 

<span data-ttu-id="a37e1-139">Voorbeeld van DNS-zone in Json-indeling:</span><span class="sxs-lookup"><span data-stu-id="a37e1-139">Sample of DNS zone in Json format:</span></span>

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "newZoneName": {
          "type": "String",
          "metadata": {
              "description": "hello name of hello DNS zone toobe created."
          }
        },
        "newRecordName": {
          "type": "String",
          "defaultValue": "www",
          "metadata": {
              "description": "hello name of hello DNS record toobe created.  hello name is relative toohello zone, not hello FQDN."
          }
        }
      },
      "resources": 
      [
        {
          "type": "microsoft.network/dnszones",
          "name": "[parameters('newZoneName')]",
          "apiVersion": "2015-05-04-preview",
          "location": "global",
          "properties": {
          }
        },
        {
          "type": "microsoft.network/dnszones/a",
          "name": "[concat(parameters('newZoneName'), concat('/', parameters('newRecordName')))]",
          "apiVersion": "2015-05-04-preview",
          "location": "global",
          "properties": 
          {
            "TTL": 3600,
            "ARecords": 
            [
                {
                    "ipv4Address": "1.2.3.4"
                },
                {
                    "ipv4Address": "1.2.3.5"
                }
            ]
          },
          "dependsOn": [
            "[concat('Microsoft.Network/dnszones/', parameters('newZoneName'))]"
          ]
        }
          ]
    }

## <a name="additional-resources"></a><span data-ttu-id="a37e1-140">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="a37e1-140">Additional resources</span></span>
<span data-ttu-id="a37e1-141">Lees Hallo [REST API-documentatie voor DNS-zones ](https://msdn.microsoft.com/library/azure/mt130626.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a37e1-141">Read hello [REST API documentation for DNS zones ](https://msdn.microsoft.com/library/azure/mt130626.aspx) for more information.</span></span>

<span data-ttu-id="a37e1-142">Lees Hallo [REST-API-documentatie voor DNS-recordsets](https://msdn.microsoft.com/library/azure/mt130627.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a37e1-142">Read hello [REST API documentation for DNS record sets](https://msdn.microsoft.com/library/azure/mt130627.aspx) for more information.</span></span>

