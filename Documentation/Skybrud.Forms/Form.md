---
order: 1
---

# Form

<table class="table details lines">
    <tr>
        <th>Extends</th>
        <td><em>Nothing</em></td>
    </tr>
    <tr>
        <th>Namespace</th>
        <td><code>Skybrud.Forms.Models</code></td>
    </tr>
</table>

The `Form` class is the main model in this package, as describes the form it self along with the fields that make up the form.

As we're typically using the package in a SPA like context, it's also possible to specify and endpoint URL to which the form should be submitted.

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
            <td><code>Title</code></td>
            <td><code>string</code></td>
            <td><code>title</code></td>
            <td>An optional title of the form.</td>
        </tr>
        <tr>
            <td><code>Url</code></td>
            <td><code>string</code></td>
            <td><code>Url</code></td>
            <td>The URL of the page where the form is shown.</td>
        </tr>
        <tr>
            <td><code>EndpointUrl</code></td>
            <td><code>string</code></td>
            <td><code>endpointUrl</code></td>
            <td>The URL for the underlying API to receive the form postback.</td>
        </tr>
        <tr>
            <td><code>Description</code></td>
            <td><code>string</code></td>
            <td><code>description</code></td>
            <td>The fields making up the form.</td>
        </tr>
    </tbody>
</table>

## Usage

A new instance of the `Form` class can be initialized like in the example below:

```csharp
@using Skybrud.Forms.Models
@using Skybrud.Forms.Models.Fields
@{

    // Initialize a new form
    Form form = new Form {
        Title = "This is my form",
        Url = "/my-page/",
        EndpointUrl = "/api/form",
        Fields = new List<FieldBase>()
    };

}
```

## JSON Output

By default, when serializing the form model to JSON, the output will look like:

```json
{
  "title": "This is my form",
  "url": "/my-page/",
  "endpointUrl": "/api/form",
  "fields": []
}
```

Properties in the C# model that is `null` will be omitted in the JSON output.