code-style
=======

Eclipse
-------
##### Gradle setup
* Add `copyEclipseSettings` task and edit `codeStylePath` to match your local path of code-style:
```
task copyEclipseSettings(type: Copy) {
    def homePath = System.properties['user.home']
    def codeStylePath = "${homePath}/projects/code-style"
    from("${codeStylePath}/eclipse/settings") {
        rename('(.*prefs).*', '$1')
    }
    into project.file('.settings')

    def suffix = project.name.endsWith('-wsdl') ? 'generated' : 'normal'
    include 'org.eclipse.*.prefs', "org.eclipse.*.prefs_${suffix}"
}
```
* Run `./gradlew copyEclipseSettings`

* (Optionally) Add eclipse plugin:
```
apply plugin: "eclipse"
```
and make `eclipse` task dependent on `copyEclipseSettings`:
```
tasks["eclipse"].dependsOn copyEclipseSettings
```
Code style settings will be applied when you generate IDE config using `eclipse` task


IntelliJ IDEA
---------------------
Import code style:
 * Settings -> Editor -> Code Style -> Java -> Manage -> Import
 * Select `idea/cronn.xml`.
 * Click on `Copy to Project`.
