---
description: API for the @astralprotocol/core package
---

# API

## Constructor

Creates a new AstralClient Instance to utilize the following functions.

**`new AstralClient(_ethAddress, _endpoint?);`**

| Name | Type | Attributes | Description |
| :--- | :--- | :--- | :--- |
| **\_ethAddress** | string | REQUIRED | The Ethereum Address of the user. |
| **\_endpoint**  | string | OPTIONAL | The Graph Endpoint. Already has a default value that can be overloaded with another endpoint. |

## Methods 

### **CreateGenesisGeoDID**

Creates a GenesisGeoDID Document. This creates a new root node for the linked data structure.

**`async createGenesisGeoDID(_typeOfGeoDID: string): Promise<IDocumentInfo>{}`**

{% tabs %}
{% tab title="Parameters" %}
| **Name** | Type  | Attributes | Description |
| :--- | :--- | :--- | :--- |
| **\_typeOfGeoDID** | GeoDidType | REQUIRED | The type of Genesis GeoDID you want to create. OfType GeoDidType. |
{% endtab %}

{% tab title="Returns" %}
| Type | Description |
| :--- | :--- |
| **IDocumentInfo** | Returns info regarding the Document Type, like the geodidid and the Document Itself.  |

```text
interface IDocumentInfo {
    geodidid: string;
    documentVal: any;
    parentid?: string;
}
```
{% endtab %}
{% endtabs %}

### **CreateChildGeoDID** 

Creates a Child GeoDIDDocument. This creates a child node for an existing linked data structure.

**`async createChildGeoDID(_typeOfGeoDID: string, _parentID: string, _path: string): Promise<IDocumentInfo>{}`**

{% tabs %}
{% tab title="Parameters" %}
| Name | Type | Attributes | Description |
| :--- | :--- | :--- | :--- |
| **\_typeOfGeoDID** | GeoDidType | REQUIRED | The type of Genesis GeoDID you want to create. OfType GeoDidType. |
| **\_parentID** | string  | REQUIRED | The Parent GeoDID ID of this new Child GeoDID |
| **\_path** | string | REQUIRED | The path that will be appended to the Parent GeoDID ID |
{% endtab %}

{% tab title="Returns" %}
| Type | Description |
| :--- | :--- |
| **DocumentInfo** | Returns information regarding the Document, like the GeoDID ID and the contents of the Document. |

```text
interface IDocumentInfo {
    geodidid: string;
    documentVal: any;
    parentid?: string;
}
```
{% endtab %}
{% endtabs %}

### **PinDocument**

Pins the Document to IPFS or FFS via Powergate.

**`async pinDocument(_documentInfo: IDocumentInfo, _token?: string): Promise<IPinInfo>{}`**

{% tabs %}
{% tab title="Parameters" %}
| Name | Type | Attributes | Description |
| :--- | :--- | :--- | :--- |
| **\_documentInfo** | IDocumentInfo | REQUIRED | The Info related to the Document that is required for pinning.  |
| **\_token** | string | OPTIONAL | The Auth Token of the Powergate Instance that you want to pin the document on. If you don't have one yet, the client will automatically create a new one for you and return it for you to save. |
{% endtab %}

{% tab title="Returns" %}
| Type | Description |
| :--- | :--- |
| **IPinInfo** | Returns information regarding the Pin, like the GeoDID ID, cid, Powergate Auth token, and the pinDate. |

```text
interface IPinInfo {
    geodidid: string;
    cid: string;
    pinDate: Date;
    token: string
} 
```
{% endtab %}
{% endtabs %}

### **LoadDocument**

Loads the Document by the DocID and the Powergate Auth token associated with it.

**`async loadDocument(_docId: string, _token: string): Promise<ILoadInfo>{}`**

{% tabs %}
{% tab title="Parameters" %}
| Name | Type | Attribute | Description |
| :--- | :--- | :--- | :--- |
| **\_docId** | string | REQUIRED | The GeoDID id of the DID Document. |
| **\_token** | string | REQUIRED | The Auth Token for the Powergate Instance that the Document in stored on.  |
{% endtab %}

{% tab title="Returns" %}
| Type | Description |
| :--- | :--- |
| **ILoadInfo** | Returns information regarding the Load, like the DocumentInfo as well as the Powergate Instance that the Document was pinned on. |

```text
interface LoadInfo {
    documentInfo: IDocumentInfo;
    powergateInstance: Powergate 
}
```
{% endtab %}
{% endtabs %}



