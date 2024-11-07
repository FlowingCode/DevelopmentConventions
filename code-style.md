## Flowing Code Style Guide / 1.0.3-rc2

In any file format, avoid using tab characters to replace a fixed amount of whitespace in any file format, as their display can differ across devices and platforms.

### Java

Apply the [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html)

#### Formatter

* Eclipse: download the [eclipse-java-google-style](https://github.com/google/styleguide/blob/gh-pages/eclipse-java-google-style.xml) formatter. Remove the preset sorting order of import statements as shown below.
* IntelliJ: install the google-java-format plugin. For further configuration and installations instructions refer to [this documentation](https://github.com/google/google-java-format/blob/master/README.md#intellij-jre-config).
* VSCode: use Google's Eclipse formatter as explained [here](https://code.visualstudio.com/docs/java/java-linting#_formatter).
* Maven: execute `mvn com.spotify.fmt:fmt-maven-plugin:format`

![image](https://user-images.githubusercontent.com/11554739/201381569-fb6afe7d-a6be-42e1-84f0-32382f0cd44b.png)

#### Local Variable Type Inference

Regarding the use of `var` (introduced in Java 10), follow the [Local Variable Type Inference Style Guidelines](https://openjdk.org/projects/amber/guides/lvti-style-guide)

- [Choose variable names that provide useful information.](https://openjdk.java.net/projects/amber/guides/lvti-style-guide#G1)
- [Minimize the scope of local variables.](https://openjdk.java.net/projects/amber/guides/lvti-style-guide#G2)
- [Consider var when the initializer provides sufficient information to the reader.](https://openjdk.java.net/projects/amber/guides/lvti-style-guide#G3)
- [Use var to break up chained or nested expressions with local variables.](https://openjdk.java.net/projects/amber/guides/lvti-style-guide#G4)
- [Take care when using var with diamond or generic methods.](https://openjdk.java.net/projects/amber/guides/lvti-style-guide#G6)
- [Take care when using var with literals.](https://openjdk.java.net/projects/amber/guides/lvti-style-guide#G7)

Prefer diamond constructor invocation (introduced in Java 7) for fields and for variables without inferred types. For instance: 
```
Map<String,List<Integer>> map = new HashMap<>();
```
Instead of:
```
Map<String,List<Integer>> map = new HashMap<String,List<Integer>>();
```
#### Early returns
Using early returns as guard clauses for handling preconditions is preferred because it enhances code readability by simplifying structure and flow, reducing cognitive load for readers, and allowing the main logic to proceed cleanly with more explicit error conditions. This approach also minimizes indentation and nesting, making the logic easier to follow, particularly in larger functions.

Example:
```
public void foo(String myString) {
   if (myString == null) {
      return;
   } 
   // Do something more here...
}
```

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

#### Deprecation

To indicate deprecation use both the `@Deprecated` annotation and the `@deprecated` JavaDoc tag.

The `@Deprecated` annotation allows tools to identify deprecated APIs, while the `@deprecated` 
tag provides documentation that explains the reasons for deprecation and suggests alternatives.

```
  /** Sets the foo.
   * @param foo the foo to be set.
   * @deprecated Use {@code setFooBar} instead.*/
  @Deprecated(forRemoval = true)
  void setFoo(Object foo) {
    // ...
  }
```
