# Introduction

This journey starts wanting to use the LUA interpreter embedded into `THE_GAME`. Which upon testing, it uses LUA version `5.1`. As a good LUA interpreter, **environmental variables** affect it. Which allows us to use **external modules**.

# Installation

`THE_GAME` runs in 32bits, thats why we install these
files in the respective order:

- LUA for Windows v5.1: [download link](https://github.com/rjpcomputing/luaforwindows/releases/download/v5.1.5-52/LuaForWindows_v5.1.5-52.exe), [ref1](https://github.com/rjpcomputing/luaforwindows/releases)
- Decompress `luarocks-3.9.1-win32.zip` (legacy Windows package, includes Lua 5.1) and run `./install.bat /F /MSVC`: [download link](http://luarocks.github.io/luarocks/releases/luarocks-3.9.1-win32.zip), [ref1](http://luarocks.github.io/luarocks/releases/), [ref2](https://github.com/luarocks/luarocks/wiki/Installation-instructions-for-Windows)

  > It should install to the default path: `C:\Program Files (x86)\LuaRocks`

  Configuration `C:\Program Files (x86)\LuaRocks\config-5.1.lua`:

  ```
  rocks_trees = {
    { name = [[user]],
         root    = home..[[/luarocks]],
    },
    { name = [[system]],
         root    = [[C:\Program Files (x86)\Lua\5.1\systree]],
    },
  }
  variables = {
      MSVCRT = 'MSVCR80',
      LUALIB = 'lua5.1.lib', --lua5.1.dll CHANGED THIS LINE
  }
  verbose = false   -- set to 'true' to enable verbose output
  ```

  > **FATAL ERROR**: This config will fix fatal error during compilation of modules `C:\Program Files (x86)\Lua\5.1\lua5.1.dll : fatal error LNK1107: invalid or corrupt file: cannot read at 0x330`.

  > Which occurs when `link -dll` of `lua5.1.dll`. _It can't create an executable by using source files or DLLs. ... For example, pass .obj, .lib, and .res files, not .cpp, .h, .dll, or .rc files._: [ref](https://docs.microsoft.com/en-us/cpp/error-messages/tool-errors/linker-tools-error-lnk1107?view=msvc-170)

- Install `Visual Studio Community 2019 v16.11.17` to compile modules with `cl.exe` for Windows: [download link](https://visualstudio.microsoft.com/vs/older-downloads/)

  > I have tested with MingW, Msys32, nothing works better than VStudio2019.

- Some modules will need LUA 5.1 headers, which we will provide with `lua-5.1.5_Win32_dll16_lib.zip`, just unzip it somewhere, in my case it was in: `D:\Prycs\lua_includes\lua-5.1.5_Win32_dll16_lib`. [download link](https://sourceforge.net/projects/luabinaries/files/5.1.5/Windows%20Libraries/Dynamic/lua-5.1.5_Win32_dll16_lib.zip/download). This path will be for `LUA_LIBDIR` and `LUA_INCDIR`.

- Environmental variables:

```
PATH
C:\Program Files (x86)\LuaRocks
```

```
LUA_CPATH
C:\Program Files (x86)\Lua\5.1\systree\lib\lua\5.1\?.dll
```

```
LUA_PATH
;;C:\Program Files (x86)\Lua\5.1\systree\share\lua\5.1\?.lua;C:\Program Files (x86)\Lua\5.1\systree\share\lua\5.1\?\init.lua
```

> It is very important to preserve the prepending `;;`

```
LUA_LIBDIR and LUA_INCDIR
D:\Prycs\lua_includes\lua-5.1.5_Win32_dll16_lib
```

# Modules

To install modules, we use `x64_x86 Cross Tools Command Prompt (Visual Studio 2019 Developer Command Prompt v16.11.17)` as Admin.

Then execute:

- luarocks install luasocket
- luarocks install lua-websocket
- luarocks install lua-cjson

# References

- https://training-course-material.com/images/1/11/Installing_LuaRocks.pdf
- https://github.com/lunarmodules/luasocket/issues/336
- https://github.com/lunarmodules/luasocket/issues/321
- https://stackoverflow.com/questions/52026115/luarocks-on-windows-not-recognizing-my-lua-libdir
