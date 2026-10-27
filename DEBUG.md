# Debugging Instructions

## Kernel Debugging

To debug the kernel, follow these steps:

1. Make sure you have the `C/C++` extension in VSCode.
2. Save this to `.vscode/launch.json` and select the right configuration depending on your OS.

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "xv6-riscv",
      "type": "cppdbg",
      "request": "launch",
      "program": "${workspaceFolder}/kernel/kernel",
      "cwd": "${workspaceFolder}",
      "MIMode": "gdb",

      // this is the macOS configuration:
      "miDebuggerPath": "/opt/homebrew/bin/riscv64-elf-gdb",
      // and this is for linux or WSL:
      "miDebuggerPath": "/usr/bin/gdb-multiarch",

      "miDebuggerServerAddress": "127.0.0.1:25501",
      "stopAtEntry": false
    }
  ]
}
```

3. In `.gdbinit.tmpl-riscv`, comment out these lines:

    ```sh
    # target remote 127.0.0.1:1234
    # symbol-file kernel/kernel
    ```

    Otherwise you will get the errors: `qemu-system-riscv64: QEMU: Terminated via GDBstub` and `Unable to start debugging. Unexpected GDB output from command "-target-select remote 127.0.0.1:25501". could not connect: Operation timed out.`

4. Install the required system packages:
   - macOS: `brew install gdb riscv64-elf-gdb`
   - Linux/WSL: `apt install gdb-multiarch`
   - On Windows you need the `WSL` VSCode extension. Then you can use the steps for Linux with WSL.

5. Use the "Run And Debug" tab in VSCode and select the `xv6-riscv` configuration and press the play button (Start Debugging) or press F5.
   To start xv6 with the debugger, run `make CPUS=1 qemu-gdb` in a terminal.
   (You can start the debugger or qemu first, it works either way.)
