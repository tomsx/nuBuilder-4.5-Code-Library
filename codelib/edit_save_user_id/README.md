## Edit Screen: Save the User Id to the Database

When saving a form, store the nuBuilder user id in a database column.

### 1. Possibility: Use the PHP BS event

Place this PHP code in the BS (Before Save) event of your form. Note that an (Input Text) Object with Id "your_user_id_input_object_id" must exist on your form.

```php

if(nuHasNoRecordID()){ // only execute for new records
	$userIdInputObject = "your_user_id_input_object_id"; 
	$userId = nuHash()['USER_ID'];
	$mainFormId = nuHash()['nuFORMdata'][0]->id;

	nuSetNuDataValue($nudata, $mainFormId, $userIdInputObject, $userId);
}

```

### 2. Possibility: Use the PHP AS event

Place this PHP code in the AS (After Save) event of your form:


```php
if(nuHasNoRecordID()){
  $qry  = "UPDATE `your_table` SET `user_id` = ? WHERE your_table_pk = ?";
  nuRunQuery($qry,["#USER_ID#", "#RECORD_ID#"]); 
}
```

☛ Replace *your_table*, *user_id* and *your_table_pk* with your values.
