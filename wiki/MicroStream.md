# MicroStream
## Type Handlers
> [docs](https://docs.microstream.one/manual/storage/addendum/specialized-type-handlers.html)

## Use with GraalVM
> add reflect-config.json to /src/main/resources/META-INF/native-image/[package]

[reflect-config.json](https://gist.github.com/14paxton/d51cc2f493b8d8f4271c0cf55f2aefab)

## Tid-Bits
### [Copy Object](https://docs.microstream.one/manual/storage/storing-data/deep-copy.html)

```java
 ObjectCopier objectCopier = ObjectCopier.New();

 Customer customer = root.getCustomer(id);

 Customer customerCopy = objectCopier.copy(customer);
```