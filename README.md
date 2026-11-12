# shell-mcp-server

A standalone C++20 Model Context Protocol (MCP) server exposing shell-command and direct-program execution tools.

## Tools

- `run_command` — executes shell commands (including shell operators).
- `run_program` — executes a program directly without a shell.

## Security

Execution is disabled unless `SAURON_SHELL_ENABLED=1` is set in the server environment. Enabling it permits local command/program execution with the server process's OS permissions. A denylist is not a security sandbox. Use only in an appropriately sandboxed environment and do not expose the server to untrusted clients.

## Dependency

The shared MCP implementation is provided by [mcpxx](https://github.com/pooriayousefi/mcpxx), pinned as a Git submodule at commit `8d3e971072c263dd5132c5b48e44c15926d21190` under `external/mcpxx`.

## Clone and build

```sh
git clone --recurse-submodules https://github.com/pooriayousefi/shell-mcp-server.git
cd shell-mcp-server
make
```

Or compile directly:

```sh
clang++ -std=c++20 -O2 -pthread -I external/mcpxx/include src/shell_mcp_tool_server.cpp -o bin/shell_mcp_tool_server
```

On Windows with MinGW, add `-lws2_32`.

## Run

Stdio (default): `./bin/shell_mcp_tool_server`

Streamable HTTP: `./bin/shell_mcp_tool_server http 127.0.0.1 8090`

Enable execution only when deliberately required:

```sh
SAURON_SHELL_ENABLED=1 ./bin/shell_mcp_tool_server
```

The HTTP endpoint is `/mcp`. Bind to loopback unless appropriate network controls are configured.

## License

Apache-2.0. See [LICENSE](LICENSE).
