# CheckboxList

<table class="table details lined">
    <tr>
        <th>Extends</th>
        <td><code>ListBase</code></td>
    </tr>
    <tr>
        <th>Namespace</th>
        <td><code>Skybrud.Forms.Models.Fields</code></td>
    </tr>
    <tr>
        <th>Type</th>
        <td><code>checkboxList</code></td>
    </tr>
</table>

The `CheckboxList` is a custom field type representing a list of checkboxes.

If multiple checkboxes are checked when submitting the form, the field's value should be a comma separated list of the values of the checked checkboxes.

## Properties

The class has the following properties:

<table class="table list border zebra">
    <thead>
        <tr>
            <th>C#&nbsp;Name</th>
            <th>C#&nbsp;Type</th>
            <th>JSON&nbsp;Name</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>Type</code></td>
            <td><code>string</code></td>
            <td><code>type</code></td>
            <td>
                <em>Inherited from the <code>FieldBase</code> class.</em><br />
                The type of the field - generally matching the HTML <c>type</c> attribute, or a custom value for non-HTML fields.
            </td>
        </tr>
        <tr>
            <td><code>Name</code></td>
            <td><code>string</code></td>
            <td><code>name</code></td>
            <td>
                <em>Inherited from the <code>FieldBase</code> class.</em><br />
                The name of the field - matching the value for the HTML `name` attribute.
            </td>
        </tr>
        <tr>
            <td><code>Label</code></td>
            <td><code>string</code></td>
            <td><code>label</code></td>
            <td>
                <em>Inherited from the <code>FieldBase</code> class.</em><br />
                A friendly name that should accompany the field.
            </td>
        </tr>
        <tr>
            <td><code>Description</code></td>
            <td><code>string</code></td>
            <td><code>description</code></td>
            <td>
                <em>Inherited from the <code>FieldBase</code> class.</em><br />
                A description that should accompany the field.
            </td>
        </tr>
        <tr>
            <td><code>IsRequired</code></td>
            <td><code>bool</code></td>
            <td><code>required</code></td>
            <td>
                <em>Inherited from the <code>FieldBase</code> class.</em><br />
                Whether the field is required/mandatory.
            </td>
        </tr>
        <tr>
            <td><code>Value</code></td>
            <td><code>object</code></td>
            <td><code>value</code></td>
            <td>
                <em>Inherited from the <code>FieldBase</code> class.</em><br />
                An optional value of the field.
            </td>
        </tr>
        <tr>
            <td><code>Items</code></td>
            <td><code>List&lt;ListItem&gt;</code></td>
            <td><code>items</code></td>
            <td>
                <em>Inherited from the <code>ListBase</code> class.</em><br />            
                The individual items making up the checkboxes of the checkbox list.
            </td>
        </tr>
    </tbody>
</table>

## JSON Output

```json
{
  "type": "checkboxList",
  "name": "myCheckBoxList",
  "label": "My checkbox list",
  "description": "A description for my checkbox list.",
  "required": true,
  "value": "1234",
  "items": [
    {
      "value": "1",
      "label": "1",
      "checked": false
    },
    {
      "value": "12",
      "label": "12",
      "checked": false
    },
    {
      "value": "123",
      "label": "123",
      "checked": false
    },
    {
      "value": "1234",
      "label": "1234",
      "checked": true
    },
    {
      "value": "12345",
      "label": "12345",
      "checked": false
    }
  ]
}
```