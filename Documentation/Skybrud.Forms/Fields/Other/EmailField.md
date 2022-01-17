# EmailField

The `EmailField` class represents a HTML `<input />` element with it's `type` attribute set to `email`. 

## Properties

The class extends the `InputField` class, thus inheriting it's properties from both `InputField` and `FieldBase`. `EmailField` doesn't have any properties of it's own.

| C#&nbsp;Name | C#&nbsp;Type  | JSON&nbsp;Name | Description                                                 |
|---------|----------|-----------|-------------------------------------------------------------|
| `Type`  | `string` | `type` | *Inherited from `FieldBase`*<br />The type of the field - generally matching the HTML `type` attribute, or a custom value for non-HTML fields. |
|  `Name`  | `string` | `name` | *Inherited from `FieldBase`*<br />The name of the field - matching the value for the HTML `name` attribute. |
|  `Label`  | `string` | `label` | *Inherited from `FieldBase`*<br />A friendly name that should accompany the field. |
|  `Description`  | `string` | `description` | *Inherited from `FieldBase`*<br />The name of the field - matching the value for the HTML `name` attribute. |
|  `IsRequired`  | `bool` | `required` | *Inherited from `FieldBase`*<br />Whether the field is required/mandatory. |
|  `Value`  | `object` | `value` | *Inherited from `FieldBase`*<br />An optional value of the field. |
| `Placeholder`  | `string` | `placeholder` | *Inherited from `InputField`*<br />The value for the HTML `placeholder` attribute |
| `Pattern`  | `string` | `pattern` | *Inherited from `InputField`*<br />The value for the HTML `pattern` attribute (aka a REGEX pattern used to validate the field). |
| `Size`  | `int?` | `size` | *Inherited from `InputField`*<br />The value for the HTML `size` attribute |