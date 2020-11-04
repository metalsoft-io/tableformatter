# golang table formatter

Utility to print pretty text (ASCII) tables. It supports:

* automatic field size adjustment
* yaml, json, CSV alternative rendering

```
This is the data I have access to
+-------+---------------------------+---------------------+-----------+--------+---------------+
| ID    | LABEL                     | OWNER               | REL.      | STATUS | DATACENTER    |
+-------+---------------------------+---------------------+-----------+--------+---------------+
| 10    | test-infrastructure       | alex@alex.com       | manager   | active | uk-reading    |
| 20    | production-infrastructure | john@alex.com       | CTO       | active | us-santaclara |
+-------+---------------------------+---------------------+-----------+--------+---------------+
Total: 2 testTbl
```


## Example

```golang
schema := []tableformatter.SchemaField{
		{
			FieldName: "ID",
			FieldType: tableformatter.TypeInt,
			FieldSize: 6,
		},
		{
			FieldName: "LABEL",
			FieldType: tableformatter.TypeString,
			FieldSize: 15,
		},
		{
			FieldName: "OWNER",
			FieldType: tableformatter.TypeString,
			FieldSize: 20,
		},
		{
			FieldName: "REL.",
			FieldType: tableformatter.TypeString,
			FieldSize: 10,
		},
		{
			FieldName: "STATUS",
			FieldType: tableformatter.TypeString,
			FieldSize: 5,
		},
		{
			FieldName: "DATACENTER",
			FieldType: tableformatter.TypeString,
			FieldSize: 10,
		},
	}

	data := [][]interface{}{
		{
			10,
			"test-infrastructure",
			"alex@alex.com",
			"manager",
			"active",
			"uk-reading",
		},
		{
			20,
			"production-infrastructure",
			"john@alex.com",
			"CTO",
			"active",
			"us-santaclara",
		},
	}

	s, err := tableformatter.RenderTable("employees", "This is the data I have access to", "text", data, schema)
	if err != nil {
		fmt.Printf("%+v", err)
	}
	fmt.Printf("%s", s)
```