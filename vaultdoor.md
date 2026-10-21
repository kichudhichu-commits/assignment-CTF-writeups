# picoCTF 2019 - vault-door-1 (Reverse Engineering)

## Challenge Metadata
- **category:** Reverse Engineering
- **Difficulty:** Medium
- **Description:** This vault uses some complicated arrays! I hope you can make sense of it, special agent.

---

## Summary
- Challenge was just unscrambling the scrambled
---

## Initial Steps

- Files given: **VaultDoor1.java**
- File type: its a java source file

---

## Procedure

- look at the strings of the given source file

```bash
strings VaultDoor1.java
```


    public boolean checkPassword(String password) {
        return password.length() == 32 &&
               password.charAt(0)  == 'd' &&
               password.charAt(29) == 'b' &&
               password.charAt(4)  == 'r' &&
               password.charAt(2)  == '5' &&
               password.charAt(23) == 'r' &&
               password.charAt(3)  == 'c' &&
               password.charAt(17) == '4' &&
               password.charAt(1)  == '3' &&
               password.charAt(7)  == 'b' &&
               password.charAt(10) == '_' &&
               password.charAt(5)  == '4' &&
               password.charAt(9)  == '3' &&
               password.charAt(11) == 't' &&
               password.charAt(15) == 'c' &&
               password.charAt(8)  == 'l' &&
               password.charAt(12) == 'H' &&
               password.charAt(20) == 'c' &&
               password.charAt(14) == '_' &&
               password.charAt(6)  == 'm' &&
               password.charAt(24) == '5' &&
               password.charAt(18) == 'r' &&
               password.charAt(13) == '3' &&
               password.charAt(19) == '4' &&
               password.charAt(21) == 'T' &&
               password.charAt(16) == 'H' &&
               password.charAt(27) == '5' &&
               password.charAt(30) == 'c' &&
               password.charAt(25) == '_' &&
               password.charAt(22) == '3' &&
               password.charAt(28) == 'e' &&
               password.charAt(26) == '4' &&
               password.charAt(31) == '3';}

---

## FLAG
On unscrambling we get text as **d35cr4mbl3_tH3_cH4r4cT3r5_45ebc3**

Flag is **academy{d35cr4mbl3_tH3_cH4r4cT3r5_45ebc3}**
    