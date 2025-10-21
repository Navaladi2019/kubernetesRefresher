# Docker: CMD vs ENTRYPOINT

## Overview

Docker provides two main instructions in a Dockerfile to define what command runs when a container starts: **CMD** and **ENTRYPOINT**. Understanding their differences and how to override them is crucial for building flexible and reusable containers.

---

## CMD

- **Purpose:**  
  Sets the default command and/or arguments to run when the container starts.
- **Behavior:**  
  - If ENTRYPOINT is not set, CMD is the command that runs.
  - If ENTRYPOINT is set, CMD provides default arguments to ENTRYPOINT.
  - CMD can be overridden by providing arguments to `docker run`.

**Example:**
```dockerfile
CMD ["echo", "Hello, World!"]
```
- Running docker run myimage → echo Hello, World!
- Running docker run myimage ls -l → ls -l


## ENTRYPOINT
- **Purpose:**  
Sets the main executable to run when the container starts.
- **Behavior:**  
 - ENTRYPOINT is always executed unless overridden with --entrypoint in docker run.
 - Arguments provided to docker run are appended to ENTRYPOINT (unless CMD is also set, which provides default arguments

```dockerfile
ENTRYPOINT ["echo", "Hello"]
```
- Running docker run myimage → echo Hello
- Running docker run myimage World! → echo Hello World!

## CMD and ENTRYPOINT Together
When both are set:

- ENTRYPOINT defines the executable.
- CMD provides default arguments.

```dockerfile
ENTRYPOINT ["echo"]
CMD ["Hello, World!"]
```
- docker run myimage → echo Hello, World!
- docker run myimage Hi → echo Hi


## Overriding CMD and ENTRYPOINT
**Override CMD**:
Provide arguments after the image name in docker run.
sh


`docker run myimage Hi`

**Override ENTRYPOINT**:
Use the --entrypoint flag in docker run.
sh


`docker run --entrypoint ls myimage -l`
This replaces the ENTRYPOINT with ls and passes -l as an argument.

## Exec Form vs Shell Form
**Exec Form (Recommended)**
Syntax: ["executable", "param1", "param2"]
Runs the command directly (no shell).
Signals (like SIGTERM) are received directly by the executable.
No shell features (like &&, |, variable expansion).

```dockerfile
ENTRYPOINT ["nginx", "-g", "daemon off;"]
```
**Shell Form**
Syntax: "executable param1 param2"
Runs the command in a shell (/bin/sh -c).
Allows shell features (like &&, |, variable expansion).
Signals are received by the shell, not the executable.

```dockerfile
ENTRYPOINT nginx -g 'daemon off;'
```

Usage statistics
Certainly! Here’s the above explanation in Markdown format, ready for your README.md:

markdown


# Docker: CMD vs ENTRYPOINT

## Overview

Docker provides two main instructions in a Dockerfile to define what command runs when a container starts: **CMD** and **ENTRYPOINT**. Understanding their differences and how to override them is crucial for building flexible and reusable containers.

---

## CMD

- **Purpose:**  
  Sets the default command and/or arguments to run when the container starts.
- **Behavior:**  
  - If ENTRYPOINT is not set, CMD is the command that runs.
  - If ENTRYPOINT is set, CMD provides default arguments to ENTRYPOINT.
  - CMD can be overridden by providing arguments to `docker run`.

**Example:**
```dockerfile
CMD ["echo", "Hello, World!"]
Running docker run myimage → echo Hello, World!
Running docker run myimage ls -l → ls -l
ENTRYPOINT
Purpose:
Sets the main executable to run when the container starts.
Behavior:
ENTRYPOINT is always executed unless overridden with --entrypoint in docker run.
Arguments provided to docker run are appended to ENTRYPOINT (unless CMD is also set, which provides default arguments).
Example:

dockerfile


ENTRYPOINT ["echo", "Hello"]
Running docker run myimage → echo Hello
Running docker run myimage World! → echo Hello World!
CMD and ENTRYPOINT Together
When both are set:

ENTRYPOINT defines the executable.
CMD provides default arguments.
Example:

dockerfile


ENTRYPOINT ["echo"]
CMD ["Hello, World!"]
docker run myimage → echo Hello, World!
docker run myimage Hi → echo Hi
Overriding CMD and ENTRYPOINT
Override CMD:
Provide arguments after the image name in docker run.
sh


docker run myimage Hi
Override ENTRYPOINT:
Use the --entrypoint flag in docker run.
sh


docker run --entrypoint ls myimage -l
This replaces the ENTRYPOINT with ls and passes -l as an argument.
Exec Form vs Shell Form
Exec Form (Recommended)
Syntax: ["executable", "param1", "param2"]
Runs the command directly (no shell).
Signals (like SIGTERM) are received directly by the executable.
No shell features (like &&, |, variable expansion).
Example:

dockerfile


ENTRYPOINT ["nginx", "-g", "daemon off;"]
Shell Form
Syntax: "executable param1 param2"
Runs the command in a shell (/bin/sh -c).
Allows shell features (like &&, |, variable expansion).
Signals are received by the shell, not the executable.
Example:

dockerfile

ENTRYPOINT nginx -g 'daemon off;'

| Instruction | Purpose | Overridable by docker run | Typical Use |
| :-- | :-- | :-- | :-- |
| ENTRYPOINT | Main command/executable | Yes, with --entrypoint | Always run this executable |
| CMD | Default arguments or command | Yes, with arguments | Default args or command |

| Form | Syntax Example | Shell Features | Signal Handling |
| :-- | :-- | :-- | :-- |
| Exec | ["executable", "param1"] | No | Direct |
| Shell | "executable param1" | Yes | Via shell |
