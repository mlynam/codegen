# Command Line Engine

## Abstract
The command line engine should be Plugin Driven and operate as a Command Tree Executor. Commands plug in.

## Plugin Driven
Each command used for the this project should be implemented as a plugin to the engine. Plugins can be loaded at runtime or embeded at compile time.

### Loaded at runtime
When the engine is invoked, it should attempt to discover plugin commands from a known directory relative to the running directory.

```
.
├── codegen.exe
└── plugins/
    ├── otter/
    │   ├── otter.json
    │   ├── assembly.dll
    │   └── data/
    └── ceramic/
``` 

## Command Tree Executor
The command line engine will compose args into a single path of operations within the possible tree of commands. Consider the following:

```json
{
    "commands": [
        {
            "name": "new",
            "descritpion": "Create a new project",
            "args": [ "-d | --directory", "-n | --name" ],
        },
        {
            "name": "generate",
            "aliases": [ "g", "gen" ],
            "args": [ "-v | --verbose", "-nt | --no-test" ],
            "commands": [
                {
                    "name": "class",
                    "aliases": [ "c" ],
                    "args": [ "-nt | --no-test" ],
                    "commands": []
                },
                {
                    "name": "service",
                    "aliases": [ "s" ],
                    "commands": []                    
                }
            ]
        }
    ]
}
```

This JSON represents a tree of commands.  The user could ask the tool to generate a new class by using 

```
> codegen generate class
``` 

and the `generate.class` command should be invoked. Arguments defined at ancestor levels should also be overridable while the command is being built.