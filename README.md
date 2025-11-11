# mise Environment Test

A demonstration project for testing [mise](https://mise.jdx.dev/) environment configuration and file precedence.

## Overview

This project demonstrates how mise handles environment variables across different configuration files and directory hierarchies. It showcases:

- Environment variable inheritance from parent to child directories
- Configuration file precedence (`mise.toml` vs `mise.my_env.toml` vs `mise.local.toml`)
- How custom environment configurations work with mise

## Project Structure

```plain
mise-env-test/
├── mise.toml              # Parent directory default config
├── mise.my_env.toml       # Parent directory custom environment
└── child/
    ├── mise.toml          # Child directory default config
    ├── mise.my_env.toml   # Child directory custom environment
    └── mise.local.toml    # Child directory local overrides
```

## Configuration Files

### Root Directory

#### mise.toml

- Sets `MY_PARENT_STUFF` environment variable

#### mise.my_env.toml

- Overrides `MY_PARENT_STUFF` with a different value
- Demonstrates custom environment configurations

### Child Directory

#### child/mise.toml

- Sets `MY_STUFF` to "mise.toml"
- Includes a `test` task that displays various environment variables

#### child/mise.my_env.toml

- Overrides `MY_STUFF` to "mise.my_env.toml"
- Sets `MY_ENV_STUFF` (only available in custom environment)

#### child/mise.local.toml

- Sets `MY_LOCAL_STUFF` for local-only configuration
- Typically not committed to version control

## Usage

### Running the Test Task

Navigate to the `child` directory and run:

```bash
cd child
mise run test
```

This will display the values of various environment variables, showing which configuration file they came from.

### Activating Custom Environment

To use the `my_env` environment configuration:

```bash
mise -E my_env run test
```

Or spawn a sub shell:

```bash
mise -E my_env en
```

## What This Demonstrates

1. **File Precedence**: How mise loads and merges configuration from multiple files
2. **Environment Inheritance**: How child directories inherit environment variables from parent directories
3. **Custom Environments**: How to define and use custom environment configurations with `mise.<env>.toml` files
4. **Local Overrides**: How `mise.local.toml` can be used for machine-specific settings

## Expected Behavior

When running `mise run test` in the child directory:

- `MY_PARENT_STUFF`: Inherited from parent directory
- `MY_STUFF`: Set by child's mise.toml or mise.my_env.toml (depending on active environment)
- `MY_LOCAL_STUFF`: Set by mise.local.toml
- `MY_ENV_STUFF`: Only available when using the my_env environment

## Learn More

- [mise Documentation](https://mise.jdx.dev/)
- [mise Configuration Files](https://mise.jdx.dev/configuration.html)
- [mise Environments](https://mise.jdx.dev/environments.html)
