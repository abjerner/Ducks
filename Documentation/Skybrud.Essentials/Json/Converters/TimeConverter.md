# TimeConverter

The {{class:Skybrud.Essentials.Json.Converters.Time.TimeConverter}} class lets you serialize and deserialize a number of different types in both .NET and within the Skybrud.Essentials package. Currently the following types are supported:

- {{see:System.DateTime}}
- {{see:System.DateTimeOffset}}
- {{see:Skybrud.Essentials.Time.EssentialsDateTime}}
- {{see:Skybrud.Essentials.Time.EssentialsTime}}
- {{see:Skybrud.Essentials.Time.EssentialsPartialDate}} *(no time, only date)*

The converter also supports a number of different standardized date and time formats:

- {{see:Skybrud.Essentials.Time.TimeFormat.Iso8601}} *(default)*  
  Indicates that the format is **ISO 8601**.
- {{see:Skybrud.Essentials.Time.TimeFormat.Rfc822}}  
  Indicates that the format is **RFC 822**.
- {{see:Skybrud.Essentials.Time.TimeFormat.Rfc2822}}  
  Indicates that the format is **RFC 2822**.
- {{see:Skybrud.Essentials.Time.TimeFormat.UnixTime}}  
  Indicates that the format is **Unix time**.

You can decorate your properties with the {{type:Newtonsoft.Json.JsonConverterAttribute}} class as shown below. The converter will use {{see:Skybrud.Essentials.Time.TimeFormat.Iso8601}} by default, but you can specify another format as well - eg. {{see:Skybrud.Essentials.Time.TimeFormat.Rfc822}}:

```c#
public class Example {
    
    [JsonConverter(typeof(TimeConverter))]
    public DateTime Iso8601 { get; set; }
    
    [JsonConverter(typeof(TimeConverter), TimeFormat.Rfc822)]
    public DateTime Rfc822 { get; set;}
    
}
```

