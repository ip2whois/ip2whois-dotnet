IP2WHOIS .NET SDK
=================

 **_Please note that this GitHub project is no longer being maintained and has been migrated to a new repository. We recommend that you use the [IP2Location.io .NET SDK](https://github.com/ip2location/ip2location-io-dotnet) going forward._**
 
This .NET library enables user to easily implement the checking of WHOIS information for a particular domain into their solution using the API from https://www.ip2whois.com. It is a WHOIS lookup api that helps users to obtain domain information, WHOIS record, by using a domain name. The WHOIS API returns a comprehensive WHOIS data such as creation date, updated date, expiration date, domain age, the contact information of the registrant, mailing address, phone number, email address, nameservers the domain is using and much more. IP2WHOIS supports the query for [1113 TLDs and 634 ccTLDs](https://www.ip2whois.com/tld-cctld-supported).

This library requires an API key to function. You may sign up for a free API key at https://www.ip2whois.com/register.

Pre-requisite
=============
Microsoft Visual Studio 2022 or later.


Installation
============
https://www.nuget.org/packages/IP2WHOIS


Usage Example
=============
### Lookup Domain Information
```C#
using Newtonsoft.Json;
using IP2WhoisComponent;

// Configures IP2WHOIS API key
string ApiKey = "YOUR_API_KEY";

IP2Whois Whois = new IP2Whois();

Whois.Open(ApiKey);

string domain = "google.com";

// Lookup domain information
var MyTask = Whois.Lookup(domain); // async API call

try
{
	var MyObj = MyTask.Result;

	// pretty-print JSON
	Console.WriteLine(JsonConvert.SerializeObject(MyObj, Formatting.Indented));

	// individual fields
	Console.WriteLine("domain: {0}", MyObj["domain"]);
	Console.WriteLine("domain_id: {0}", MyObj["domain_id"]);
	Console.WriteLine("status: {0}", MyObj["status"]);
	Console.WriteLine("create_date: {0}", MyObj["create_date"]);
	Console.WriteLine("update_date: {0}", MyObj["update_date"]);
	Console.WriteLine("expire_date: {0}", MyObj["expire_date"]);
	Console.WriteLine("domain_age: {0}", MyObj["domain_age"]);
	Console.WriteLine("whois_server: {0}", MyObj["whois_server"]);

	var Registrar = MyObj["registrar"];
	Console.WriteLine("registrar => iana_id: {0}", Registrar["iana_id"]);
	Console.WriteLine("registrar => name: {0}", Registrar["name"]);
	Console.WriteLine("registrar => url: {0}", Registrar["url"]);

	var Registrant = MyObj["registrant"];
	Console.WriteLine("registrant => name: {0}", Registrant["name"]);
	Console.WriteLine("registrant => organization: {0}", Registrant["organization"]);
	Console.WriteLine("registrant => street_address: {0}", Registrant["street_address"]);
	Console.WriteLine("registrant => city: {0}", Registrant["city"]);
	Console.WriteLine("registrant => region: {0}", Registrant["region"]);
	Console.WriteLine("registrant => zip_code: {0}", Registrant["zip_code"]);
	Console.WriteLine("registrant => country: {0}", Registrant["country"]);
	Console.WriteLine("registrant => phone: {0}", Registrant["phone"]);
	Console.WriteLine("registrant => fax: {0}", Registrant["fax"]);
	Console.WriteLine("registrant => email: {0}", Registrant["email"]);

	var Admin = MyObj["admin"];
	Console.WriteLine("admin => name: {0}", Admin["name"]);
	Console.WriteLine("admin => organization: {0}", Admin["organization"]);
	Console.WriteLine("admin => street_address: {0}", Admin["street_address"]);
	Console.WriteLine("admin => city: {0}", Admin["city"]);
	Console.WriteLine("admin => region: {0}", Admin["region"]);
	Console.WriteLine("admin => zip_code: {0}", Admin["zip_code"]);
	Console.WriteLine("admin => country: {0}", Admin["country"]);
	Console.WriteLine("admin => phone: {0}", Admin["phone"]);
	Console.WriteLine("admin => fax: {0}", Admin["fax"]);
	Console.WriteLine("admin => email: {0}", Admin["email"]);

	var Tech = MyObj["tech"];
	Console.WriteLine("tech => name: {0}", Tech["name"]);
	Console.WriteLine("tech => organization: {0}", Tech["organization"]);
	Console.WriteLine("tech => street_address: {0}", Tech["street_address"]);
	Console.WriteLine("tech => city: {0}", Tech["city"]);
	Console.WriteLine("tech => region: {0}", Tech["region"]);
	Console.WriteLine("tech => zip_code: {0}", Tech["zip_code"]);
	Console.WriteLine("tech => country: {0}", Tech["country"]);
	Console.WriteLine("tech => phone: {0}", Tech["phone"]);
	Console.WriteLine("tech => fax: {0}", Tech["fax"]);
	Console.WriteLine("tech => email: {0}", Tech["email"]);

	var Billing = MyObj["billing"];
	Console.WriteLine("billing => name: {0}", Billing["name"]);
	Console.WriteLine("billing => organization: {0}", Billing["organization"]);
	Console.WriteLine("billing => street_address: {0}", Billing["street_address"]);
	Console.WriteLine("billing => city: {0}", Billing["city"]);
	Console.WriteLine("billing => region: {0}", Billing["region"]);
	Console.WriteLine("billing => zip_code: {0}", Billing["zip_code"]);
	Console.WriteLine("billing => country: {0}", Billing["country"]);
	Console.WriteLine("billing => phone: {0}", Billing["phone"]);
	Console.WriteLine("billing => fax: {0}", Billing["fax"]);
	Console.WriteLine("billing => email: {0}", Billing["email"]);

	Console.WriteLine("nameservers: {0}", MyObj["nameservers"]);
}
catch (Exception ex)
{
	Console.WriteLine(ex.Message);
}
```


### Convert Normal Text to Punycode
```C#
using IP2WhoisComponent;

// Convert normal text to punycode
string domain = "täst.de";
Console.WriteLine(IP2Whois.GetPunycode(domain));
```


### Convert Punycode to Normal Text
```C#
using IP2WhoisComponent;

// Convert punycode to normal text
string domain = "xn--tst-qla.de";
Console.WriteLine(IP2Whois.GetNormalText(domain));
```


### Get Domain Name
```C#
using IP2WhoisComponent;

// Get domain name from URL
string url = "https://www.example.com/exe";
Console.WriteLine(IP2Whois.GetDomainName(url));
```


### Get Domain Extension
```C#
using IP2WhoisComponent;

// Get domain extension (gTLD or ccTLD) from URL or domain name
string str = "example.com";
Console.WriteLine(IP2Whois.GetDomainExtension(str));
```


Response Parameter
==================
### Domain WHOIS Lookup function
| Parameter | Type | Description |
|---|---|---|
|domain|string|Domain name.|
|domain_id|string|Domain name ID.|
|status|string|Domain name status.|
|create_date|string|Domain name creation date.|
|update_date|string|Domain name updated date.|
|expire_date|string|Domain name expiration date.|
|domain_age|integer|Domain name age in day(s).|
|whois_server|string|WHOIS server name.|
|registrar.iana_id|string|Registrar IANA ID.|
|registrar.name|string|Registrar name.|
|registrar.url|string|Registrar URL.|
|registrant.name|string|Registrant name.|
|registrant.organization|string|Registrant organization.|
|registrant.street_address|string|Registrant street address.|
|registrant.city|string|Registrant city.|
|registrant.region|string|Registrant region.|
|registrant.zip_code|string|Registrant ZIP Code.|
|registrant.country|string|Registrant country.|
|registrant.phone|string|Registrant phone number.|
|registrant.fax|string|Registrant fax number.|
|registrant.email|string|Registrant email address.|
|admin.name|string|Admin name.|
|admin.organization|string|Admin organization.|
|admin.street_address|string|Admin street address.|
|admin.city|string|Admin city.|
|admin.region|string|Admin region.|
|admin.zip_code|string|Admin ZIP Code.|
|admin.country|string|Admin country.|
|admin.phone|string|Admin phone number.|
|admin.fax|string|Admin fax number.|
|admin.email|string|Admin email address.|
|tech.name|string|Tech name.|
|tech.organization|string|Tech organization.|
|tech.street_address|string|Tech street address.|
|tech.city|string|Tech city.|
|tech.region|string|Tech region.|
|tech.zip_code|string|Tech ZIP Code.|
|tech.country|string|Tech country.|
|tech.phone|string|Tech phone number.|
|tech.fax|string|Tech fax number.|
|tech.email|string|Tech email address.|
|billing.name|string|Billing name.|
|billing.organization|string|Billing organization.|
|billing.street_address|string|Billing street address.|
|billing.city|string|Billing city.|
|billing.region|string|Billing region.|
|billing.zip_code|string|Billing ZIP Code.|
|billing.country|string|Billing country.|
|billing.phone|string|Billing phone number.|
|billing.fax|string|Billing fax number.|
|billing.email|string|Billing email address.|
|nameservers|array|Name servers|

```json
{
	"domain": "locaproxy.com",
	"domain_id": "1710914405_DOMAIN_COM-VRSN",
	"status": "clientTransferProhibited https://icann.org/epp#clientTransferProhibited",
	"create_date": "2012-04-03T02:34:32Z",
	"update_date": "2021-12-03T02:54:57Z",
	"expire_date": "2024-04-03T02:34:32Z",
	"domain_age": 4055,
	"whois_server": "whois.godaddy.com",
	"registrar": {
		"iana_id": "146",
		"name": "GoDaddy.com, LLC",
		"url": "https://www.godaddy.com"
	},
	"registrant": {
		"name": "Registration Private",
		"organization": "Domains By Proxy, LLC",
		"street_address": "DomainsByProxy.com",
		"city": "Tempe",
		"region": "Arizona",
		"zip_code": "85284",
		"country": "US",
		"phone": "+1.4806242599",
		"fax": "+1.4806242598",
		"email": "Select Contact Domain Holder link at https://www.godaddy.com/whois/results.aspx?domain=LOCAPROXY.COM"
	},
	"admin": {
		"name": "Registration Private",
		"organization": "Domains By Proxy, LLC",
		"street_address": "DomainsByProxy.com",
		"city": "Tempe",
		"region": "Arizona",
		"zip_code": "85284",
		"country": "US",
		"phone": "+1.4806242599",
		"fax": "+1.4806242598",
		"email": "Select Contact Domain Holder link at https://www.godaddy.com/whois/results.aspx?domain=LOCAPROXY.COM"
	},
	"tech": {
		"name": "Registration Private",
		"organization": "Domains By Proxy, LLC",
		"street_address": "DomainsByProxy.com",
		"city": "Tempe",
		"region": "Arizona",
		"zip_code": "85284",
		"country": "US",
		"phone": "+1.4806242599",
		"fax": "+1.4806242598",
		"email": "Select Contact Domain Holder link at https://www.godaddy.com/whois/results.aspx?domain=LOCAPROXY.COM"
	},
	"billing": {
		"name": "",
		"organization": "",
		"street_address": "",
		"city": "",
		"region": "",
		"zip_code": "",
		"country": "",
		"phone": "",
		"fax": "",
		"email": ""
	},
	"nameservers": [
		"vera.ns.cloudflare.com",
		"walt.ns.cloudflare.com"
	]
}
```


LICENCE
=====================
See the LICENSE file.
