# C++ Builder MCP Server

An MCP server providing C++ DLL compilation and analysis capabilities. This server enables building C++ DLLs with specific export settings and analyzing DLL exports using Visual Studio build tools.

## Features

- C++ DLL compilation with MSBuild
- Custom export settings via .def files
- DLL export analysis using dumpbin
- Configurable build settings
- Platform and configuration targeting
- Detailed build output

## Tools

### DLL Compilation

#### compile_dll
Compile a C++ DLL with specific export settings using MSBuild.
- **projectPath**: Path to the .vcxproj file (required)
- **configuration**: Build configuration (optional)
  - Values: 'Debug' or 'Release'
  - Default: 'Release'
- **platform**: Target platform (optional)
  - Values: 'x86' or 'x64'
  - Default: 'x86'
- **defFile**: Path to .def file for exports (optional)
  - Specifies exported functions and their attributes
  - Used to control which functions are exposed by the DLL

The tool uses Visual Studio's MSBuild to compile the DLL, providing:
- Full build output with warnings and errors
- Support for different configurations and platforms
- Module definition file integration
- Detailed build logs

### Export Analysis

#### analyze_exports
Analyze exports from a compiled DLL using dumpbin.
- **dllPath**: Path to the DLL file (required)

The analysis provides:
- List of all exported functions
- Export ordinals
- Function names and addresses
- Export forwarding information
- Detailed export table analysis

## Requirements

- Visual Studio 2022 Community Edition or higher
- Visual C++ build tools
- Windows SDK

## Installation

1. Clone the repository:
```bash
git clone https://github.com/yourusername/cpp-builder-mcp-server.git
cd cpp-builder-mcp-server
```

2. Install dependencies:
```bash
npm install
```

3. Build the project:
```bash
npm run build
```

## Configuration

Add the server to your MCP settings file:

```json
{
  "mcpServers": {
    "cpp-builder": {
      "command": "node",
      "args": ["path/to/cpp-builder-mcp-server/dist/index.js"],
      "env": {}
    }
  }
}
```

## Usage Examples

### Compile DLL

```typescript
// Basic compilation
await mcp.use("cpp-builder", "compile_dll", {
  projectPath: "./src/MyLibrary.vcxproj"
});

// Compilation with specific settings
await mcp.use("cpp-builder", "compile_dll", {
  projectPath: "./src/MyLibrary.vcxproj",
  configuration: "Debug",
  platform: "x64",
  defFile: "./src/exports.def"
});
```

### Analyze DLL Exports

```typescript
await mcp.use("cpp-builder", "analyze_exports", {
  dllPath: "./bin/Release/MyLibrary.dll"
});
```

## Development

1. Make changes to the source code
2. Run tests:
```bash
npm test
```
3. Build the project:
```bash
npm run build
```

## Contributing

1. Fork the repository
2. Create your feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## License

MIT