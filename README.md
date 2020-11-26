# Adding-Subform-Rows-on-Zoho-CRM
An elegant script that allows you to add rows into a subform without overwriting existing row(s).

## Core Idea
Here's an easy yet effective way of adding rows to subforms via Deluge without overwriting existing ones.

## Tutorial

### Create a Map for the New Row
Create a map with the subform column API names (key) and the respective values. 
```javascript
updateMap = Map();
updateMap.put("Product","Apples");
updateMap.put("Quantity","50");
updateMap.put("Price","2");
```
*Note: Replace the API name of the subform fields accordingly.*

### Add the Map into a List
A list format is required to update subforms. Create a list and add the *updateMap* variable into it.

```javascript
updateList = List();
updateList.add(updateMap);
```

### Get All Existing Subform Row ID(s) and Add to the List
To prevent existing data in the subform from being overwritten, iterate through every existing row on the subform, create a map of the IDs, and then add to the *updateList* variable.
```javascript
record = zoho.crm.getRecordById("INSERT_MODULE_API_NAME", "INSERT_RECORD_ID");
subform = record.get("INSERT_SUBFORM_API_NAME");
for each s in subform
{
	updateList.add({"id":s.get("id")});
}
```

### Update CRM
Update the subform on the CRM record with the *updateList* variable that you have made.
```javascript
updateCRM = zoho.crm.updateRecord("INSERT_MODULE_API_NAME", "INSERT_RECORD_ID" , {"INSERT_SUBFORM_API_NAME" : updateList});
info updateCRM;
```
