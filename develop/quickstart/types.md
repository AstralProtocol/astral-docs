---
description: Common Types used throughout the Project
---

# Types

#### IDocumentInfo

```text
interface IDocumentInfo {
    geodidid: string;
    documentVal: any;
    parentid?: string;
}
```

**ILoadInfo**

```text
interface LoadInfo {
    documentInfo: IDocumentInfo;
    powergateInstance: Powergate 
}
```

**IPinInfo**

```text
interface IPinInfo {
    geodidid: string;
    cid: string;
    pinDate: Date;
    token: string
} 
```

