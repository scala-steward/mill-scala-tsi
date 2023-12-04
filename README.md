# mill-scala-tsi
Mill plugin for Scala TSI, ported from [scala-tsi](https://github.com/scala-tsi/scala-tsi).

## Installation

```scala
import io.github.hoangmaihuy.scalatsi._

object example extends ScalaModule with ScalaTsiModule {
      // The classes that you want to generate typescript interfaces for
      override def typescriptExports = Seq("MyClass")
      // The output file which will contain the typescript interfaces
      override def typescriptOutputFile = millSourcePath / "model.ts"
      // Include the package(s) of the classes here
      // Optionally import your own TSType implicits to override default default generated
      override def typescriptGenerationImports = Seq("mymodel._", "MyTypescript._")
}
```

Now `mill example.generateTypescript` will transform a file like
```scala
case class MyClass(foo: String, bar: Int)
```

Into a typescript interface like
```typescript
export interface IMyClass {
  foo: string
  bar: number
}
```

## Configuration

| Key | Type           | Default               | Description |
| --- |----------------|-----------------------| ----------- |
| typescriptExports | Seq[String]    | `Seq()`               | A list of all your (top-level) classes that you want to generate interfaces for |
| typescriptGenerationImports | Seq[String]    | `Seq()`               | A list of all imports. This should import all classes you defined above, as well as custom `TSType` implicits |
| typescriptOutputFile | os.Path        | `T.dest/scala-tsi.ts` | The output file with generated typescript interfaces |
| typescriptStyleSemicolons | Boolean        | `false`               | Whether to add semicolons to the exported model |
| typescriptHeader | Option[String] | `Some("...")`         | A header for the output file. Contains a notice about the file being generated by default |
| typescriptTaggedUnionDiscriminator | Option[String] | `Some("type")`        | The discriminator field for tagged unions, or None to disable tagged unions |

## More information

You can go to [scala-tsi](https://github.com/scala-tsi/scala-tsi) for more documentation and examples of the project.

## Licenses

This software is released under the Apache License 2.0. More information in the file LICENSE distributed with this project.