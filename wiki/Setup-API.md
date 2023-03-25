### Add API to workspace

The API for developers can be found on [CurseForge](https://www.curseforge.com/minecraft/mc-mods/project-arsenal/files) (as additional file(s)) in two formats: ``api`` and ``api-sources``.
The former is the compiled version, and the latter is the original source-code version, which includes the javadocs.

#### Step 1: CurseMaven repository
First of all, in order to use the API we need to add it to our workspace.
For this we'll need to have [CurseMaven](https://www.cursemaven.com) to be defined in the ``repositories`` (the one for dependencies) block of our ``build.gradle``:
````gradle
repositories {
    maven {
        url = "https://www.cursemaven.com"
    }
}
````

#### Step 2: Add the API as a dependency
To make sure Project Arsenal's API will **only be available at compilation**, and not while running the game, we'll be using Gradle's [``compileOnly``](https://docs.gradle.org/current/userguide/declaring_dependencies.html) for this:
````gradle
dependencies {
    /* Minecraft dependency here */
    
    // {api_id} needs to be replaced with the file id of the API file found on CurseForge
    // {api-sources_id} needs to be replaced with the file id of the API Sources file found on CurseForge
    compileOnly fg.deobf('curse.maven:project-arsenal-api-683122:{api_id}-sources-{api-sources_id}')
}
````

> When appending the file id with ``-sources-{file_id}``, the sources file will automatically layer on top of the regular jar.
> This step is recommend as the sources jar includes the javadocs for the API.

> File id's for version **0.3.3** of the API are as follows:
> * ``1.19.3-api``: ``4454978``, ``1.19.3-api-sources``: ``4454979``
> * ``1.19.2-api``: ``4454975``, ``1.19.2-api-sources``: ``4454976``
> * ``1.18.2-api``: ``4454973``, ``1.18.2-api-sources``: ``4454974``
> * ``1.16.5-api``: ``4454971``, ``1.16.5-api-sources``: ``4454972``

#### Step 3: Define dependency in mods.toml
An optional dependency for Project Arsenal can be defined (in the ``mods.toml``) like this:
````toml
[[dependencies.your_mod_id]]
    modId="projectarsenal"
    mandatory=false # or 'true' if you simply want your users to always have Project Arsenal installed
    versionRange="[0.3.1,)"
    ordering="NONE"
    side="BOTH"
````

> **Tip:** You can tell users of your mod that there's Project Arsenal integration simply by adding [Project Arsenal](https://www.curseforge.com/minecraft/mc-mods/project-arsenal) as an "Optional dependency" on CurseForge.

#### Step 4: Add main mod jar for testing (OPTIONAL!)
You can add Project Arsenal's main jar **for testing** to your development environment as well:
````gradle
dependencies {
    /* ...other dependencies */
    
    // {file_id} needs to be replaced with the file of the main jar found on CurseForge
    runtimeOnly fg.deobf('curse.maven:project-arsenal-683122:{file_id}')
}
````

> It is recommended to only add Project Arsenal's main jar as ``runtimeOnly`` dependency, and to only use it for testing out the features.
> After testing it is better to **remove the main jar** again.

***

* [Introduction](./Developers)
* *Add API to workspace*
* [Implement API features](./Implement-API)

