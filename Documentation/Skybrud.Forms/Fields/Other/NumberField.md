# NumberField

<table class="table details lined">
    <tr>
        <th>Extends</th>
        <td><code>FieldBase</code></td>
    </tr>
    <tr>
        <th>Namespace</th>
        <td><code>Skybrud.Forms.Models.Fields</code></td>
    </tr>
    <tr>
        <th>Type</th>
        <td><code>number</code></td>
    </tr>
</table>

The `NumberField` class represents a HTML `<input />` element with it's `type` attribute set to `number`. 

## Properties

The class extends the `NumberField` class, thus inheriting it's properties from both `NumberField` and `NumberField`.

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
            <td><code>Placeholder</code></td>
            <td><code>string</code></td>
            <td><code>placeholder</code></td>
            <td>
                <em>Inherited from the <code>InputField</code> class.</em><br />
                The value for the HTML <code>placeholder</code> attribute.
            </td>
        </tr>
        <tr>
            <td><code>Pattern</code></td>
            <td><code>bool</code></td>
            <td><code>pattern</code></td>
            <td>
                <em>Inherited from the <code>InputField</code> class.</em><br />
                The value for the HTML <code>pattern</code> attribute (aka a REGEX pattern used to validate the field).
            </td>
        </tr>
        <tr>
            <td><code>Size</code></td>
            <td><code>int?</code></td>
            <td><code>size</code></td>
            <td>
                <em>Inherited from the <code>InputField</code> class.</em><br />
                The value for the HTML <code>size</code> attribute.
            </td>
        </tr>
        <tr>
            <td><code>Min</code></td>
            <td><code>int?</code></td>
            <td><code>min</code></td>
            <td>The minimum allowed value.</td>
        </tr>
        <tr>
            <td><code>Max</code></td>
            <td><code>int?</code></td>
            <td><code>max</code></td>
            <td>The maximum allowed value.</td>
        </tr>
    </tbody>
</table>

## JSON Output

```json
{
  "type": "number",
  "name": "numberField",
  "label": "A number",
  "description": "Enter a number between 1-10.",
  "required": true,
  "min": 1,
  "max": 9,
  "placeholder": "Enter a number between 1-10.",
  "pattern": "[1-9]",
  "size": 9001,
  "value": 7
}
```