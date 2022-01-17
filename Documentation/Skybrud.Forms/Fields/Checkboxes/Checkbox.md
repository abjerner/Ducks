# Checkbox

<table class="table details lined">
    <tr>
        <th>Extends</th>
        <td><code>ButtonBase</code></td>
    </tr>
    <tr>
        <th>Namespace</th>
        <td><code>Skybrud.Forms.Models.Fields</code></td>
    </tr>
    <tr>
        <th>Type</th>
        <td><code>checkbox</code></td>
    </tr>
</table>

The `Checkbox` class represents a single checkbox similar to writing `<input type="checkbox" />` in HTML.

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
            <td><code>IsChecked</code></td>
            <td><code>bool</code></td>
            <td><code>checked</code></td>
            <td>A boolean value indicating whether the checkbox should initially be checked.</td>
        </tr>
    </tbody>
</table>

## JSON Output

```json
{
  "type": "checkbox",
  "name": "iCanHasBacon",
  "label": "I can has bacon?",
  "description": "A description about whether Bjerner absolutely should have bacon (he should).",
  "checked": true,
  "required": true,
  "value": "yup"
}
```