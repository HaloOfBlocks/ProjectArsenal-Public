### Implement API features

As of version **0.3.1**, the API includes the following features:
* **Fire Mode Selector**: Allows setting a fire mode selector  on existing guns
* **Hud Overlay**: Applies a simple overlay with ammo counter and (if applicable) selected fire mode

> **Tip:** Each feature is registered through an event. You can check their javadocs for more information.

#### Step 1: Special class for Project Arsenal API features
Simply create a class named something like ``ProjectArsenalCompat`` or ``ProjectArsenalIntegration`` with a ``public`` constructor.
This class will contain all our code from Project Arsenal's API.
We'll have to tell Forge's Event Bus to register this class for events, **but only when Project Arsenal is loaded**.
We can do this simply by adding the following code in our main class's (class annotated with ``@Mod``) constructor:
````java
if (ModList.get().isLoaded("projectarsenal"))
{
    MinecraftForge.EVENT_BUS.register(new ProjectArsenalCompat());
}
````

#### Step 2: Register a feature
As an example, we'll be registering a fire mode selector for a gun.
For this we'll need to utilize the ``RegisterFireModesEvent`` provided by the API.
````java
@SubscribeEvent
public void registerFireModes(RegisterFireModesEvent event)
{
    event.register(MyItems.MY_GUN.get(), FireModeSelector.set(FireModes.FULL_AUTOMATIC, FireModes.SAFETY));
}
````

> Step 2 can be replicated for other events as well.
> See their respective javadocs for more information.

***

* [Introduction](./Developers)
* [Add API to workspace](./Setup-API)
* *Implement API features*

