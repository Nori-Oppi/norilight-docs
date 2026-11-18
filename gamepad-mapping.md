# Gamepad mapping

Norilight reads controllers through [SDL](https://www.libsdl.org), which needs a mapping to
know which button is which. Mappings for most controllers ship with Norilight, and it
downloads a newer list from the community
[SDL_GameControllerDB](https://github.com/mdqinc/SDL_GameControllerDB) at each start.
A controller without one isn't sent to the host, and Norilight warns about it.

## First try

- **Restart Norilight** with the controller connected, after updating it: the list may
  have the controller now.
- **Use a different mode.** Many controllers have an XInput (Xbox) mode, often a switch or a
  button held while connecting. XInput controllers always work on Windows.
- **Steam Input** can turn any controller into a virtual Xbox controller; add Norilight to
  Steam as a non-Steam game and start it from there.

## Making a mapping

1. Download the [SDL2 Gamepad Tool](https://generalarcade.com/gamepadtool/) and open it
   with the controller connected.
2. Choose the controller, press **Create a new mapping**, and press each button it asks for.
3. Press **Copy Mapping String**.
4. Give it to Norilight once: quit Norilight, then start it with the mapping in the
   `SDL_GAMECONTROLLERCONFIG` environment variable. In a Command Prompt, in Norilight's
   the folder that holds `Norilight.exe`:

   ```
   set SDL_GAMECONTROLLERCONFIG=<the mapping string>
   Norilight.exe
   ```

   On macOS:
   `SDL_GAMECONTROLLERCONFIG='<the mapping string>' /Applications/Norilight.app/Contents/MacOS/Norilight`

Norilight saves the mapping in its settings, so later starts don't need the variable. A
[reset](https://github.com/Nori-Oppi/Norilight/blob/main/docs/GUIDE.md#resetting-norilight)
moves it to the backup with the other settings.

Consider adding the mapping to
[SDL_GameControllerDB](https://github.com/mdqinc/SDL_GameControllerDB) as well, so it reaches
everyone.

## On the host

The game on the host sees an emulated Xbox, DualShock 4 or Switch controller. Which one is
set per app (the gamepad type in Norishine's app editor) or for the whole host in its input
settings. Games that use a DualShock 4's touchpad or motion sensors need that type.
