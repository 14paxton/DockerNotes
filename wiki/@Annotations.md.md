# Annotations
## Quick Snippets
### Generate UUID identity
```java
 @Id
    @Column(columnDefinition = "BINARY(16)")
    @GeneratedValue(generator = "system-uuid", strategy = GenerationType.IDENTITY)
    @GenericGenerator(name = "system-uuid", strategy = "org.hibernate.id.UUIDGenerator")
```

## Core
### [io.micronaut.core.annotation](https://docs.micronaut.io/3.4.2/api/index.html?io/micronaut/core/annotation/package-summary.html)

Blocking | A marker annotation for methods that are blocking.
-- | --
Creator | An annotation applicable to a constructor that provides a hint as to which constructor is the primary constructor.
EntryPoint | EntryPoint is a meta-annotation used on other annotations to indicate that the annotated element is an entry point into the framework from the outside.
Experimental | Annotates a class or method as being experimental and subject to change or removal.
Generated | A marker annotation for methods that are generated though an annotation processor.
Indexed | An annotation that can be used on types where there may be many implementations of a particular interface.
Indexes | Allows Indexed to be repeatable.
InstantiatedMember | An annotation that can be used on another annotation member that returns a class to indicate that the value of the annotation should be populated as an instance of the specified class.
Internal | Annotates a class or method regarded as internal and not for public consumption.
Introspected | An annotation that indicates a type should produce a BeanIntrospection at compilation time.
Introspected.IndexedAnnotation | Allow pre-computed indexes for property lookups based on an annotation and a member.
NonBlocking | A marker annotation for methods that are non-blocking.
NonNull | A common annotation to declare that annotated elements cannot be null.
Nullable | A common annotation to declare that annotated elements can be null under some circumstance.
Order | Annotation for objects that are ordered.
ReflectiveAccess | Descriptive annotation that can be used to declare a field, method, constructor and types for reflective access.
TypeHint | The type hint annotation is a general annotation that can be used on interfaces to provide additional information about types used at runtime.
UsedByGeneratedCode | A marker annotation indicating that a method is used by generated code and should not be modified or removed otherwise a binary compatibility problem will be introduced.

---

## [Data](https://micronaut-projects.github.io/micronaut-data/latest/guide/) 
### [io.micronaut.data.annotation](https://micronaut-projects.github.io/micronaut-data/1.0.x/api/io/micronaut/data/annotation/package-summary.html)


Annotation Type | Description
-- | --
AutoPopulated | Meta annotation to identity annotations that are auto-populated by the Micronaut Data.
DataTransformer | Generic version of allowing transformations to be applied when reading or writing data to and from the a database.
DateCreated | Can be applied to date type to indicate the property should be populated when it is first inserted.
DateUpdated | Can be applied to date type to indicate the property should be populated when it was last updated.
Embeddable | Annotation to be used on POJOs that are embeddable in MappedEntity types.
EmbeddedId | Annotation that specifies the embedded ID.
GeneratedValue | Designates a property as a generated value.
Id | Designates a field or method that is annotated with the Id of an entity.
Join | A @Join defines how a join for a particular association path should be generated.
MappedEntity | Designates a class as being persisted.
MappedProperty | Designates a method or field that is mapped as a persistent property.
Query | Defines the query string such as SQL, JPA-QL, Cypher etc that should be executed.
QueryHint | Provides a query hint to the underlying query implementation.
Relation | Annotation used to indicate a field or method is a relation to another type.
Repository | Designates a type of a data repository.
RepositoryConfiguration | Models compilation time configuration for the repository.
Transient | Annotation used to indicate a field or method is transient and not persisted.
TypeDef | Type definitions allow associated existing types with a specify DataType.
TypeRole | A type role indicates a method element in a repository that plays a role in query execution and should not be factored into query calculation but instead made available at runtime using the specified role name.
Version | Designates a field or method that is used to version an entity.
Where | There Where annotation allows augmenting the WHERE statement of generated queries with additional criterion.


***In the case of using JPA only a subset of annotations are supported including the following:***

- Basic: @Table @Id @Version @Column @Transient @Enumerated

- Embedded definition: @Embedded @EmbeddedId @Embeddable

- Relationship mapping: @OneToMany @OneToOne @ManyToOne @ManyToMany

- Join specification: @JoinTable @JoinColumn

- Type converters: @Convert @Converter and AttributeConverter interface


---

## Validation
### [javax.validation.constraints](https://docs.jboss.org/hibernate/beanvalidation/spec/2.0/api/javax/validation/constraints/package-summary.html)


Annotation Type | Description
-- | --
AssertFalse | The annotated element must be false.
AssertFalse.List | Defines several AssertFalse annotations on the same element.
AssertTrue | The annotated element must be true.
AssertTrue.List | Defines several AssertTrue annotations on the same element.
DecimalMax | The annotated element must be a number whose value must be lower or equal to the specified maximum.
DecimalMax.List | Defines several DecimalMax annotations on the same element.
DecimalMin | The annotated element must be a number whose value must be higher or equal to the specified minimum.
DecimalMin.List | Defines several DecimalMin annotations on the same element.
Digits | The annotated element must be a number within accepted range.
Digits.List | Defines several Digits annotations on the same element.
Email | The string has to be a well-formed email address.
Email.List | Defines several @Email constraints on the same element.
Future | The annotated element must be an instant, date or time in the future.
Future.List | Defines several Future annotations on the same element.
FutureOrPresent | The annotated element must be an instant, date or time in the present or in the future.
FutureOrPresent.List | Defines several FutureOrPresent annotations on the same element.
Max | The annotated element must be a number whose value must be lower or equal to the specified maximum.
Max.List | Defines several Max annotations on the same element.
Min | The annotated element must be a number whose value must be higher or equal to the specified minimum.
Min.List | Defines several Min annotations on the same element.
Negative | The annotated element must be a strictly negative number (i.e.
Negative.List | Defines several Negative constraints on the same element.
NegativeOrZero | The annotated element must be a negative number or 0.
NegativeOrZero.List | Defines several NegativeOrZero constraints on the same element.
NotBlank | The annotated element must not be null and must contain at least one non-whitespace character.
NotBlank.List | Defines several @NotBlank constraints on the same element.
NotEmpty | The annotated element must not be null nor empty.
NotEmpty.List | Defines several @NotEmpty constraints on the same element.
NotNull | The annotated element must not be null.
NotNull.List | Defines several NotNull annotations on the same element.
Null | The annotated element must be null.
Null.List | Defines several Null annotations on the same element.
Past | The annotated element must be an instant, date or time in the past.
Past.List | Defines several Past annotations on the same element.
PastOrPresent | The annotated element must be an instant, date or time in the past or in the present.
PastOrPresent.List | Defines several PastOrPresent annotations on the same element.
Pattern | The annotated CharSequence must match the specified regular expression.
Pattern.List | Defines several Pattern annotations on the same element.
Positive | The annotated element must be a strictly positive number (i.e.
Positive.List | Defines several Positive constraints on the same element.
PositiveOrZero | The annotated element must be a positive number or 0.
PositiveOrZero.List | Defines several PositiveOrZero constraints on the same element.
Size | The annotated element size must be between the specified boundaries (included).
Size.List | Defines several Size annotations on the same element.

---

## Hibernate

<div class="sect4" style="box-sizing: border-box; margin: 0px; padding: 0px; direction: ltr; color: rgba(0, 0, 0, 0.8); font-family: &quot;Noto Serif&quot;, &quot;DejaVu Serif&quot;, serif; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; background-color: rgb(255, 255, 255); text-decoration-thickness: initial; text-decoration-style: initial; text-decoration-color: initial;">

Annotation | Purpose
-- | --
@Entity | Declares an entity class (a class with its own database table an persistent identity)
@MappedSuperclass | A superclass that declares common persistent fields of its @Entity subclasses
@Embeddable or @Embedded | Declare an embeddable class (a class without its own persistent identity or database table)
@Inheritance | Defines how inheritance hierarchies should be mapped to database tables
@Id | Specifies that a field of an entity holds the persistent identity of the entity, and maps to the primary key of its table
@IdClass | Specifies a class representing the composite primary key of the entity (for entities with multiple @Id fields)
@EmbeddedId | Specifies that a field of an entity holds its composite primary key represented as an @Embeddable class
@GeneratedValue | Specifies that an identifier is a system-generated surrogate key
@Version | Specifies that a field of an entity holds a version number used for optimistic locking
@Enumerated | Maps a field holding an enum
@ManyToOne | Declares a many-to-one association to a second entity
@OneToOne | Declares a one-to-one association to a second entity
@OneToMany | Declares a one-to-many association to a second entity
@Table | Specifies a mapping to a database table
@SecondaryTable | Specifies a mapping to a second database table
@Column | Specifies a mapping to a database column
@JoinColumn | Specifies a mapping to a database foreign key
@Cache | Enables second-level caching for an entity
@Formula | Maps field to SQL expression instead of a column
@CreationTimestamp, @UpdateTimestamp | Automatically assign a timestamp to a field
@OptimisticLocking | Enables optimistic locking for entities with no @Version field
@FilterDef and @Filter | Define a Hibernate filter
@FetchProfile | Defines a Hibernate fetch profile
@Generated | Defines a property generated by the database
@ColumnDefault | Specifies a SQL expression used to assign a default value to a column (use in combination with @Generated(INSERT))
@GenericGenerator | Selects a custom id generator
@DynamicInsert and @DynamicUpdate | Generate SQL dynamically with only needed columns (instead of using static SQL generated at startup)
@Fetch | Specifies the fetching mode for an association
@BatchSize | Specifies the batch size for batch fetching an association
@Loader | Specifies a named query used to fetch an entity by id (for example, when find(type, id) is called) in place of the default SQL generated by Hibernate
@SqlInsert, @SqlUpdate, @SqlDelete | Specify custom DML for entity operations
@NaturalId | Marks a field or fields as an alternative "natural" identifier (unique key) of the entity
@Nationalized | Use nchar, nvarchar, or nclob selectively for one particular column.
@Immutable | Specifies that an entity or collection is immutable
@SortNatural or @SortComparator | Maps a SortedSet or SortedMap
@Check | Declares a SQL check constraint to be added to DDL


</div>

Hibernate Type | Database Type | JDBC Type | Type Registry
-- | -- | -- | --
org.hibernate.type.StringType | string | VARCHAR | string, java.lang.String
org.hibernate.type.MaterializedClob | string | CLOB | materialized_clob
org.hibernate.type.TextType | string | LONGVARCHAR | text
org.hibernate.type.CharacterType | char, java.lang.Character | CHAR | char, java.lang.Character
org.hibernate.type.BooleanType | boolean | BIT | boolean, java.lang.Boolean
org.hibernate.type.NumericBooleanType | boolean | INTEGER, 0 is false, 1 is true | numeric_boolean
org.hibernate.type.YesNoType | boolean | CHAR, ‘N’/’n’ is false, ‘Y’/’y’ is true. The uppercase value is written to the database. | yes_no
org.hibernate.type.TrueFalseType | boolean | CHAR, ‘F’/’f’ is false, ‘T’/’t’ is true. The uppercase value is written to the database. | true_false
org.hibernate.type.ByteType | byte, java.lang.Byte | TINYINT | byte, java.lang.Byte
org.hibernate.type.ShortType | short, java.lang.Short | SMALLINT | short, java.lang.Short
org.hibernate.type.IntegerTypes | int, java.lang.Integer | INTEGER | int, java.lang.Integer
org.hibernate.type.LongType | long, java.lang.Long | BIGINT | long, java.lang.Long
org.hibernate.type.FloatType | float, java.lang.Float | FLOAT | float, java.lang.Float
org.hibernate.type.DoubleType | double, java.lang.Double | DOUBLE | double, java.lang.Double
org.hibernate.type.BigIntegerType | java.math.BigInteger | NUMERIC | big_integer
org.hibernate.type.BigDecimalType | java.math.BigDecimal | NUMERIC | big_decimal, java.math.bigDecimal
org.hibernate.type.TimestampType | java.sql.Timestamp | TIMESTAMP | timestamp, java.sql.Timestamp
org.hibernate.type.TimeType | java.sql.Time | TIME | time, java.sql.Time
org.hibernate.type.DateType | java.sql.Date | DATE | date, java.sql.Date
org.hibernate.type.CalendarType | java.util.Calendar | TIMESTAMP | calendar, java.util.Calendar
org.hibernate.type.CalendarDateType | java.util.Calendar | DATE | calendar_date
org.hibernate.type.CurrencyType | java.util.Currency | VARCHAR | currency, java.util.Currency
org.hibernate.type.LocaleType | java.util.Locale | VARCHAR | locale, java.utility.locale
org.hibernate.type.TimeZoneType | java.util.TimeZone | VARCHAR (Using the TimeZone ID) | timezone, java.util.TimeZone
org.hibernate.type.UrlType | java.net.URL | VARCHAR | url, java.net.URL
org.hibernate.type.ClassType | java.lang.Class | VARCHAR (Using the class name) | class, java.lang.Class
org.hibernate.type.BlobType | java.sql.Blob | BLOB | blog, java.sql.Blob
org.hibernate.type.ClobType | java.sql.Clob | CLOB | clob, java.sql.Clob
org.hibernate.type.BinaryType | primitive byte[] | VARBINARY | binary, byte[]
org.hibernate.type.MaterializedBlobType | primitive byte[] | BLOB | materized_blob
org.hibernate.type.ImageType | primitive byte[] | LONGVARBINARY | image
org.hibernate.type.BinaryType | java.lang.Byte[] | VARBINARY | wrapper-binary
org.hibernate.type.CharArrayType | char[] | VARCHAR | characters, char[]
org.hibernate.type.CharacterArrayType | java.lang.Character[] | VARCHAR | wrapper-characters, Character[], java.lang.Character[]
org.hibernate.type.UUIDBinaryType | java.util.UUID | BINARY | uuid-binary, java.util.UUID
org.hibernate.type.UUIDCharType | java.util.UUID | CHAR, VARCHAR | uuid-char
org.hibernate.type.PostgresUUIDType | java.util.UUID | PostgreSQL UUID | pg-uuid
org.hibernate.type.SerializableType | Implementors of java.lang.Serializable | VARBINARY | Unlike the other value types, multiple instances of this type are registered. It is registered once under java.io.Serializable and registered under the specific java.io.Serializable implementation class names


---

## Lombok
### ***Needs to be above micronaut annotations on classpath in gradle***
```groovy
  annotationProcessor 'org.projectlombok:lombok:1.18.24'
```

### ***For lombok to recognize micronaut annotations and inject into constructor***

> create lombok.config at root, insert line:
> 
>> ```propeties
>>    lombok.copyableannotations += io.micronaut.core.annotation.Nullable
>> ```