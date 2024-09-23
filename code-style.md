## Flowing Code Style Guide / 1.0.3-rc1

### Java

Apply the [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html)

* Eclipse: download the [eclipse-java-google-style](https://github.com/google/styleguide/blob/gh-pages/eclipse-java-google-style.xml) formatter. Remove the preset sorting order of import statements as shown below.
* IntelliJ: install the google-java-format plugin. For further configuration and installations instructions refer to [this documentation](https://github.com/google/google-java-format/blob/master/README.md#intellij-jre-config).
* VSCode: use Google's Eclipse formatter as explained [here](https://code.visualstudio.com/docs/java/java-linting#_formatter).
* Maven: execute `mvn com.spotify.fmt:fmt-maven-plugin:format`

![image](https://user-images.githubusercontent.com/11554739/201381569-fb6afe7d-a6be-42e1-84f0-32382f0cd44b.png)

### JavaDoc

Apply the [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html#s7-javadoc) (Section 7)

#### When to use `{@code}`

Prefer `{@code}` over `<code>`, unless the code contains a closing brace (`}`).

In each comment, the first occurrence of an identifier that refers to a class, field, or method must be enclosed in a `{@link}` tag. Otherwise, the identifier must be wrapped in `{@code}` (or `<code>` see #39).

The following identifiers must never be linked and should always be wrapped in `{@code}:`
- The name of the type being documented, or the type where the documented method/field is located.
- The names of the field type, method return type, and argument types.
- Exceptions listed in the throws` clause of the documented method.
- The names of the direct supertype and any implemented interfaces of the documented type (in a type-level comment).

```
  /**
   * Creates a new instance of {@code FooBar}.
   */
  public FooBar() { ... }
```