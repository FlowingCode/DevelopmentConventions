## Flowing Code Style Guide / 1.0.2

### Java

Apply the [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html)

* Eclipse: download the [eclipse-java-google-style](https://github.com/google/styleguide/blob/gh-pages/eclipse-java-google-style.xml) formatter. Remove the preset sorting order of import statements as shown below.
* IntelliJ: install the google-java-format plugin. For further configuration and installations instructions refer to [this documentation](https://github.com/google/google-java-format/blob/master/README.md#intellij-jre-config).
* VSCode: use Google's Eclipse formatter as explained [here](https://code.visualstudio.com/docs/java/java-linting#_formatter).
* Maven: execute `mvn com.spotify.fmt:fmt-maven-plugin:format`

![image](https://user-images.githubusercontent.com/11554739/201381569-fb6afe7d-a6be-42e1-84f0-32382f0cd44b.png)
