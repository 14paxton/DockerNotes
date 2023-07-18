# [Jackson](https://github.com/FasterXML/jackson-docs)

## Text Manipulation

### toString and toMap
```java
    @JsonValue
    @Override
   public Map<String, Object> toMap() {
        Map<String, Object> raw = new HashMap<>();
        raw.put("yourField", this.yourField.toPlainString());
        /* more fields */
        return raw;
    }

    @JsonValue
    @Override
    public String toString() {
        // add JSON processing exception handling, dropped for readability
        return new ObjectMapper().writeValueAsString(this.toMap());
    }
```

#### Pass a string as JSON
```java
public class Data {
    private Map<String, User> record;

    public Map<String, User> getRecord() { return record; }

    public void setRecord(Map<String, User> record) { this.record = record; }

    @Override
    public String toString() {
        return "Data{" +
                "record=" + record +
                '}';
    }
}
```

### JSON string to JsonNode
```java
Map<String, Object> agencyMap = Map.of(
        "name", "Agencia Prueba",
        "phone1", "1198788373",
        "address", "Larrea 45 e/ calligaris y paris",
        "number", 267,
        "enable", true,
        "location", Map.of("id", 54),
        "responsible", Set.of(Map.of("id", 405)),
        "sellers", List.of(Map.of("id", 605))
);
ObjectNode agencyNode = new ObjectMapper().valueToTree(agencyMap);
```

## Common Config Settings
```yml
jackson:
  property-naming-strategy: LOWER_CAMEL_CASE
  locale: en_US
  date-format: yyyy-MM-dd'T'HH:mm:ss.SSS
  mapper:
    ACCEPT_CASE_INSENSITIVE_ENUMS: true
  serialization:
    INDENT_OUTPUT: false
    WRITE_DATE_TIMESTAMPS_AS_NANOSECONDS: false
    WRITE_DATES_AS_TIMESTAMPS: false
  deserialization:
    FAIL_ON_UNKNOWN_PROPERTIES: false
    READ_DATE_TIMESTAMPS_AS_NANOSECONDS: false
  serialization-inclusion: non_null
``` 

# References

### [jackson feature docs](https://github.com/FasterXML/jackson-databind/wiki/JacksonFeatures)
#### [micronaut jackson config docs](https://docs.micronaut.io/latest/guide/#_jackson_configuration)

## Examples

- [Annotations](https://www.baeldung.com/jackson-advanced-annotations)
- [More Annotations](https://www.baeldung.com/jackson-annotations#bd-3-jsonanysetter)