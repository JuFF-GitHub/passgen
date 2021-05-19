# Passgen

Made with Bash. The script should just run on the standard Linux distros - no further installation necessary.

### Purpose

Passgen is meant to generate strong, valid, random-looking passwords deterministically from any given text-string or key. *<u>You don't need to remember or store the generated password, because you can always generate it as long as you remember the text-string you provided</u>*. There lies its security. To generate the same password on a different machine, however, you'd need to note down the PASSGEN_SALT that is output.

### Security model

Every password generation requires an effectively single-threaded process that takes a significant time (mostly <1m though). This is because the algorithm uses a [Hashcash](https://en.bitcoin.it/wiki/Hashcash)-like [proof-of-work](https://en.bitcoin.it/wiki/Proof_of_work) procedure with target SHA-512 <2^509. The algorithm is so designed that a minimum amount of work must always be done. 

Also, it cannot be predicted beforehand exactly how much time the password generation would take. For some values of the given text-string, the time taken may be way over the 1m mark. Hopefully, this unpredictability and requirement of single-threadedness would make brute-force hacks slow.

### Usage

<u>*Non-interactive:*</u>

```bash
timeout <max number of seconds you can have your patience e.g. 60> \
./passgen [-w <no. of chars in the desired password>] <string that you can remember>
```

Example: 

1. `timeout 60 ./passgen -w 10 'Iluvbash'`
2. `timeout 60 ./passgen 'patience is a virtue'`

*<u>Interactive</u>:*

```bash
timeout 60 ./passgen
```

**Tip:** If password generation is taking too much time, try some other text-string.

### Features:

1. Passwords are bound to the device they are generated on, if the environment variable `PASSGEN_SALT` is not set. In other words, when `PASSGEN_SALT` has no value, running `passgen` on the same machine will always output the same password and take nearly the same time, but running it on different machines will give different output and require different times. Therefore, to generate the same password in similar time in two different machines, do `export PASSGEN_SALT=<your chosen value>` before running `passgen`.
2. Every password essentially contains at least one special character, one upper-case letter, one lower-case letter and one numeral. The default width for generated passwords is 8 characters.

