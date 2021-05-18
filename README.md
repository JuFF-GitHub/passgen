# Passgen

Made with Bash. Should just run on Linux - no further installation necessary.

### Purpose

To generate random-looking passwords deterministically from any given text-string. Every password generation requires >100 ms because the algorithm uses a basic Proof-of-Work with SHA-512 <2^510.

### Usage

```bash
./passgen <string that you can remember> <no. of chars in the desired password>
```

**Tip:** If password generation is taking too much time, try some other string.

### Feature:

Passwords are bound to the device they are generated on. In other words, running the above code on the same machine will always output the same password and take nearly the same time, but running it on different machines will give different output and require different times.