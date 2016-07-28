# Command
## Abstract
Commands are strongly typed classes that are exercised by the [engine](https://github.com/mlynam/codegen/blob/master/docs/design/engine.md). Commands should be packaged with a metadata file to describe usage, arguments, aliases, and command name.

## Metadata
### Example
```json
{
    "name": "generate",
    "description": "Generates a code files for a construct.",
    "args": [
        {
            "name": "no-test",
            "shorthand": "nt",
            "description": "The construct is generated without unit tests. We do not recommend
                            this as a practice",
            "optional": true,
            "default": false
        }
    ]
}
```

## Abstraction
We want to use an abstract class here because we expect to have ```ctor``` initialization logic. A command must define the methods described in the example.
### Example
```csharp
public abstract class Command
{
    public Command()
    {
        // Load the metadata file and initialize the Command
    }

    public abstract Initialize(CommandBuilder builder);
    public abstract Execute(ExecutionContext context);
}
```
