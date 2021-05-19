# Passgen

Made with Bash. The script should just run on the standard Linux distros - no further installation necessary.

### Purpose

To generate random-looking passwords deterministically from any given text-string. Every password generation requires an effectively single-threaded process and takes a significant time (mostly <1m though) because the algorithm uses a basic [Hashcash](https://en.bitcoin.it/wiki/Hashcash)-like [proof-of-work](https://en.bitcoin.it/wiki/Proof_of_work) procedure with target SHA-512 <2^509. Also, it cannot be predicted beforehand, exactly how much time the algorithm would take - for some values of the given text-string, the time taken may be way over the 1m mark. This unpredictability and requirement of single-threadedness should make brute-force hacks slow.

### Usage

*Non-interactive:*

```bash
timeout <max number of seconds you can have your patience> \
./passgen <string that you can remember> <no. of chars in the desired password>
```

*Interactive:*

```bash
timeout 60 ./passgen
```

**Tip:** If password generation is taking too much time, try some other string.

### Feature:

Passwords are bound to the device they are generated on if the environment variable `PASSGEN_SALT` is not set. In other words, when `PASSGEN_SALT` has no value, running `passgen` on the same machine will always output the same password and take nearly the same time, but running it on different machines will give different output and require different times. Therefore, to generate the same password in similar time in two different machines, do `export PASSGEN_SALT=<your chosen value>` before running `passgen`.

