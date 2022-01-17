# Button

<table class="table details lines">
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
        <td><code>button</code></td>
    </tr>
</table>

The `Button` class represents a normal HTML button similar to writing `<button type="button"></button>`.

## Properties

The class has the following properties:

<table class="table list border">
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
    </tbody>
</table>

## Usage

The package supports a few different ways to add a button - eg. via an extension method directly on the form:

```csharp
form.AddButton("myButton", "My button");
```

The extension method doesn't support all properties available for a button, but adds a shortcut for easier adding simple buttons.

For a bit more control, you can initialize a new `Button` class and add it the the form's `Fields` property:

```csharp
form.Fields.Add(new Button {
    Name = "myButton",
    Label = "My button",
    IsRequired = true,
    Description = "This button is required, although this is a little weird for a button.",
    Value = "I can has value?"
});
```

## JSON Output

In it's simplest form, a button field will be serialized to JSON as:

```json
{
  "type": "button",
  "name": "myButton",
  "label": "My button"
}
```

but with more properties specified, it may look like this:

```csharp
{
  "type": "button",
  "name": "myButton",
  "label": "My button",
  "description": "This button is required, although this is a little weird for a button.",
  "required": true,
  "value": "I can has value?"
}
```
