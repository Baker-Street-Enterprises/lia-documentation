
# Customizing Plugins

Plugins allow for extending the functionality of LIA beyond it's original scope without requiring prior programming 
knowledge. There are a set of configuration values that can be passed to the plugin(s) for customizing what data is 
passed on to the third party or internal service. 

# Search Table Dropdown Menu Plugins
Plugins provide the following functionality within the context of the "***search_index_option_column.json***" 
functionality:

###### Open an external web page 

**Example :** Opens the ICANN registry and shows information about the domain linked to the downloaded content. 
```json
  {
    "label": "ICANN Domain Lookup",
    "url": "https://lookup.icann.org/lookup?q={Domain}"
  }
```

**Example :** Opens the Web Archive's history on the URL where the content was found. 

```json
  {
    "label": "Web Archive",
    "url": "https://web.archive.org/web/*/{Url}"
  }
```

###### Fetch/Get Content from Enrichment service

**Example :** An synonymous way of posting the Domain name, ie ({Domain} vs {ContentDomain}) linked to the captured 
content. This service enriches the Capture by providing "tags" that categorize the domain. 

*IMPORTANT* : YOU MUST have the attribute "cmd" set to "ProxyContent"
```json
  {
    "label": "Get Domain Categorization",
	"url": "http://lia.enrichment.vm:8000/domain/categorization/who-is-xml-api/{ContentDomain}",
	"method": "GET",
	"cmd": "ProxyContent"
  }
```

###### POST Content from Enrichment service or to third party service for further analysis, distribution or persistence

**Example :** Posts all the data about the captured content to a third party web service internally hosted system.

*IMPORTANT* : YOU MUST have the attribute "cmd" set to "ProxyContent"
```json
  {
	  "cmd": "ProxyContent",
	  "label": "Passthru",
	  "url": "http://lia.enrichment.vm:8000/passthru/",
	  "method": "POST",
	  "mode": "cors",
	  "cache": "default",
	  "credentials": "omit",
	  "headers": {
		"Content-Type": "application/x-www-form-urlencoded"
	  },
	  "redirect": "follow",
	  "referrerPolicy": "no-referrer-when-downgrade",
	  "lia": {},
	  "data": {}
  }  
```

### Search Table Options Customizations

The search table located on the main app page has a set of dropdown menu items that can be customized. Let's check out 
the default set of options. 
```json
[
  {
    "label": "View Html Version (Default View)",
    "url": "http://localhost:9906/html/{Uuid}.html"
  },
  {
    "label": "Live Page",
    "url": "{Url}"
  },
  {
    "label": "View Raw",
    "url": "http://localhost:9906/raw/{Uuid}"
  },
  {
    "label": "View as MHTML",
    "url": "{Uuid}",
    "cmd": "GetMhtmlPage"
  },
  {
    "label": "Web Archive",
    "url": "https://web.archive.org/web/*/{Url}"
  },
  {
    "label": "ICANN Domain Lookup",
    "url": "https://lookup.icann.org/lookup?q={Domain}"
  },
  {
    "label": "Proxy Forwarding",
    "cmd": "ProxyContent",
	"id": "{Id}",
	"fieldName": "file",
	"url": "http://lia.enrichment.vm:8000/upload-file/"	
  },
  {
    "label": "Get Domain Categorization",
	"url": "http://lia.enrichment.vm:8000/domain/categorization/who-is-xml-api/{ContentDomain}",
	"method": "GET",
	"cmd": "ProxyContent"
  },
  {
	  "cmd": "ProxyContent",
	  "label": "Passthru",
	  "url": "http://lia.enrichment.vm:8000/passthru/",
	  "method": "POST",
	  "mode": "cors",
	  "cache": "default",
	  "credentials": "omit",
	  "headers": {
		"Content-Type": "application/x-www-form-urlencoded"
	  },
	  "redirect": "follow",
	  "referrerPolicy": "no-referrer-when-downgrade",
	  "lia": {},
	  "data": {}
  }  
]
```

# Post Processing Plugins
A similar implementation technique to "Search Table Dropdown Menu Plugins", but the "Post Processing Plugins" add
the ability to forward data after it has been persisted locally to a third party service automatically. 

**Example :** Automatically fetch the domain categorization for the most recently captured content. 

***IMPORTANT*** The "cmd" value is the command that "this" plugin will run for.  

```json
  {
    "label": "Get Domain Categorization",
	"url": "http://lia.enrichment.vm:8000/domain/categorization/who-is-xml-api/{ContentDomain}",
	"method": "GET",
	"cmd": "SaveAsset"
  }
```

**Example :** Automatically push the saved content up to a third party server.

```json
  {
	  "cmd": "SaveAsset",
	  "label": "Passthru",
	  "url": "http://lia.enrichment.vm:8000/passthru/",
	  "method": "POST",
	  "mode": "cors",
	  "cache": "default",
	  "credentials": "omit",
	  "headers": {
		"Content-Type": "application/x-www-form-urlencoded"
	  },
	  "redirect": "follow",
	  "referrerPolicy": "no-referrer-when-downgrade",
	  "lia": {},
	  "data": {}
  } 
```


# Plugin Data Variables
Here is a comprehensive list of variables that are available within the context of the "Post Processing Plugins"
```

```





