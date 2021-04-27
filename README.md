# ReactTable
Generic React Table Component

Dependencies
---

- "react": "17.0.1"
- "tailwindcss": "^2.0.3"
- "nanoid": "^3.1.22"

Usage
---

Component props:

- properties!
- className?
- customRenderers?
- actions?

Assuming we give a list 'items' of objects with the following fields:

```
{
  field1, field2, field3, field4
}
```

Each field present on each object in the list 'items' that is defined on 'properties' will be automatically rendered on the table as is.

If a field is present on 'customRenderers' (optional), that field rendering is left to be customized by passing a callback in the form (item: T) => React.Node

If the property 'actions' is defined, an aditional column 'Actions' is added, and for each row, the given list containing render callbacks in the form (item: T) => React.Node is executed. This is most frequently used to add Action Buttons for each item. 

Complete example below:

```
<Table
    className="w-full table-auto"
    properties={{
        field1: 'Field One Label',
        field2: 'Field Two Label',
        field3: 'Field Three Label',
        field4: 'Field Four Label',
    }}
    items={items}
    customRenderers={{
        field1: (item) => {
            return (
                <TextInput
                    className="w-full"
                    value={item.field1}
                    data={item}
                    onChange={onItemField1Changed}
                />
            )
        },
        field2: (item) => {
            return (
                <Select
                    data={item}
                    defaultValue={item.field2.id}
                    options={options.map((op) => {
                        return {
                            label: op.name.toUpperCase(),
                            value: op.id,
                        }
                    })}
                    onChange={onItemField2Changed}
                />
            )
        }
    }}
    actions={[
        (item) => {
            return (
                <button
                    className="px-5 py-2 bg-blue-500 rounded-lg text-white"
                    onClick={() => {
                        console.log(item.field1)
                    }}
                >
                    Action 1
                </button>
            )
        },
        ,
        (item) => {
            return (
                <button
                    className="px-5 py-2 bg-blue-500 rounded-lg text-white"
                    onClick={() => {
                        console.log(item.field2)
                    }}
                >
                    Action 2
                </button>
            )
        },
    ]}
  />
```
