code-style
=======

Eclipse
-------
##### Gradle setup
* Add `copyEclipseSettings` task and edit `codeStylePath` to match your local path of code-style:
```
task downloadEclipseSettings(type: Download) {
    def baseUrl = "https://raw.githubusercontent.com/mbazanski/code-style/master/eclipse/settings/"
    src([
        baseUrl + 'org.eclipse.core.resources.prefs',
        baseUrl + 'org.eclipse.jdt.core.prefs_normal',
        baseUrl + 'org.eclipse.jdt.ui.prefs',
    ])
    dest project.file('.settings')
}

task copyEclipseSettings(type: Copy) {
    dependsOn downloadEclipseSettings

    from project.file('.settings')
    into project.file('.settings')

    rename("org.eclipse.jdt.core.prefs_normal", "org.eclipse.jdt.core.prefs")
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
