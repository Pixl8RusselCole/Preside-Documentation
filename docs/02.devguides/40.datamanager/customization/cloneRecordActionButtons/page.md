---
id: datamanager-customization-clonerecordactionbuttons
title: "Data Manager customization: cloneRecordActionButtons"
---

## Data Manager customization: cloneRecordActionButtons

The `cloneRecordActionButtons` customization allows you to completely override the form action buttons (e.g. "Cancel", "Add record") for the clone record form. The handler is expected to return a string that is the rendered HTML and is provided the following in the `args` struct:

* `objectName`: The name of the object
* `recordId`: The ID of the record being cloneed
* `record`: Struct of the record being cloneed
* `cloneRecordAction`: URL for submitting the form
* `draftsEnabled`: Whether or not drafts are enabled
* `canSaveDraft`: Whether or not the current user can save drafts (for drafts only)
* `canPublish`: Whether or not the current user can publish (for drafts only)
* `cancelAction`: URL that any rendered 'cancel' link should use

For example:


```luceescript
// /application/handlers/admin/datamanager/GlobalDefaults.cfc
component {

	private string function cloneRecordActionButtons( event, rc, prc, args={} ) {
		var objectName = args.objectName ?: "";
		
		args.cancelAction = event.buildAdminLink( objectName=objectName );

		return renderView( view="/admin/datamanager/globaldefaults/cloneRecordActionButtons", args=args );
	}

}
```

```lucee
<!--- /application/views/admin/datamanager/globaldefaults/cloneRecordActionButtons.cfm --->

<cfoutput>
	<div class="col-md-offset-2">
		<a href="#args.cancelAction#" class="btn btn-default" data-global-key="c">
			<i class="fa fa-reply bigger-110"></i>
			Cancel
		</a>
		
		<button type="submit" class="btn btn-info" tabindex="#getNextTabIndex()#">
				<i class="fa fa-save bigger-110"></i> Save record
		</button>
	</div>
</cfoutput>
```

>>>> The core implementation has logic for showing different buttons for drafts and dynamically building labels for buttons, etc. Be sure to know what you're missing out on when overriding this (or any) customization!

