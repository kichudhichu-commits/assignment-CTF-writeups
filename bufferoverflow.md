# picoCTF(2022) Buffer Overflow 0 (pwn)

## Challenge Metadata
- **Category:** Pwn
- **Difficulty:** Medium
- **Source:** `vuln.c`

---

## Summary
- The program reads a line into `buf1` using `gets()`.
- It passes that input to `vuln()`, where `strcpy()` copies it into a smaller 16-byte buffer.
- A sufficiently long input can corrupt the stack and cause a segmentation fault.
- The program installs a `SIGSEGV` handler that prints the flag stored in `flag`.

---

## Initial Steps

- **Inspecting the source code:**

  ```c
  void vuln(char *input) {
      char buf2[16];
      strcpy(buf2, input);
  }
  ```

- `buf2` is only 16 bytes long, while `strcpy()` copies the input without checking its length. This creates a stack-based buffer overflow.

- In `main()`, the program sets up a signal handler:

  ```c
  signal(SIGSEGV, sigsegv_handler);
  ```

- The handler prints the contents of `flag` when a segmentation fault occurs:

  ```c
  void sigsegv_handler(int sig) {
      printf("%s\n", flag);
      fflush(stdout);
      exit(1);
  }
  ```

---

## Exploitation

- **Understanding the input flow:**

  ```text
  gets(buf1) -> vuln(buf1) -> strcpy(buf2, input)
  ```

  Although `buf1` is 100 bytes, the later copy into `buf2[16]` is not length-checked.

- **Triggering the handler:**

  The goal is to provide input long enough to corrupt the stack and cause `SIGSEGV`. When the handler runs, it prints the flag read from `flag.txt`.


- **Connecting to the remote instance:**



 
 ```bash
  nc chatelaine.cylabacademy.net 16328

Input: iwdshuIEAHfiUHsfu9hSOughoGU
academy{ov3rfl0ws_ar3nt_that_bad_eb3cbdf1}
```




## Flag

The `SIGSEGV` handler prints the flag loaded from the instance's `flag.txt` when a segmentation fault occurs.

**Flag value:** **academy{ov3rfl0ws_ar3nt_that_bad_eb3cbdf1}**
