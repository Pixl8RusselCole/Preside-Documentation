---
id: datamanager-customization-getquickaddrecordformname
title: "Data Manager customization: getQuickAddRecordFormName"
---

## Data Manager customization: getQuickAddRecordFormName

>>> This customization was added in Preside 10.13.0

The `getQuickAddRecordFormName` customization allows you to use a different form name than the Data Manager default for "quick adding" records. The method should return the form name (see [[presideforms]]) and is provided `args.objectName` should you need to use it. For example:

```luceescript
// /application/handlers/admin/datamanager/blog.cfc

component {

	private string function getQuickAddRecordFormName( event, rc, prc, args={} ) {
		return "admin.blogs.addblog";
	}

}
```

