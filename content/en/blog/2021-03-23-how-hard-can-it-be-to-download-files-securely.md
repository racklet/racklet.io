---
author: luxas
date: 2021-03-23 08:30:00+00:00
title: How hard can it be to download files securely?
description: Introducing Racklet!
url: /blog/2021/03/how-hard-can-it-be-to-download-files-securely
---

[![hackmd-github-sync-badge](https://hackmd.io/yvmhvTMhRn6c61mey87I2Q/badge)](https://hackmd.io/yvmhvTMhRn6c61mey87I2Q)


[TOC]

Let's in this case assume that you are a client that wants to download an image from a server.

You could do this with:

```bash
# Download the file from the server
wget http://server-ip.com/my-image.jpg
# View the picture (on the desktop) using "Eye of GNOME Image Viewer"
eog my-image.jpg
```

(if you did not know of these commands before, check [`wget`] and [`eog`] out now)

[`eog`]: https://help.gnome.org/users/eog/stable/
[`wget`]: https://www.gnu.org/software/wget/

However, that leaves your software system open to a large variety of attacks. We'll explore _some_ of those below.

Now, for those who are thinking about this example, don't put too much focus on the example being an image, or the delivery mechanism, HTTP. Just think in the abstract sense of "I need to download something, and I need it to match the content I aimed to get".

For those who are interested, though, check this [Stackoverflow post] out, or this article on the [Steganography] technique.

[Stackoverflow post]: https://security.stackexchange.com/questions/53958/malicious-code-in-image-harmful
[Steganography]: https://www.sentinelone.com/blog/hiding-code-inside-images-malware-steganography/

## Attack Vectors when downloading only one file

In this section, I'd like to first focus on the attack vectors that are present when the program is just downloading _one single file_. Downloading multiple related files, complicates things even more, so we'll save that for later.

### Tracking/Surveillance

Potentially malicious observers (e.g. in the same network) of the program may be able to read the request

(DNS over TLS) => Encryption

### Endless data attacks

=> Metadata separately

### Corrupt data
(e.g. flip one or some bytes) in order to DoS => Checksum

### Arbitrary (malicious) content
=> Checksum and Signatures

### Key compromise
=> Multiple keys, create a trusted chain, set expiration timestamps
### Indefinite freeze attacks

=> Timestamping and expiration of metadata


## Foundations

### Integrity

When you are done with downloading the file, how do you know that the file actually is the one you expect? Say that you have some prior information about what the file you expect should look like. Then you need some way to check if the downloaded data actually matches the prior information.

If you **do not** check if what you just downloaded matches the expectations, you can't verify the integrity of the file. If so, you can't ensure the file is a) the one you expected, or b) non-corrupt (say, a bit could have flipped during the transportation).

Commonly, in software systems, the prior information in this case is a [`checksum`] (also denoted `hash`, `hash value` or `message digest`). A checksum is the output of a [`hash function`].

A hash function `H(message) = checksum` has three main properties:

1. Non-reversible (one way only): It is practically infeasible to reconstruct `message` with only knowledge about `checksum`.
2. Fixed-length output: The length of `checksum` is the same, regardless of the length of `message`.
3. Collision resistent[^collision-resistance]: It is practically infeasible to find two different `message` inputs that produce the exact same `checksum`.

[^collision-resistance]: In case you're wondering how much time it would take to guess, at random, a message that produces a 256-bit checksum, check this video out: [How large is 2^256 by 3Blue1Brown]

What can you do with a hash function?

1. Check whether two (potentially large) files are the equal, without comparing them bit-by-bit
2. Check if [passwords match], without never store the password in plaintext in a database
3. Verify the integrity of a file, to make sure no bit has flipped
4. Create [digital signatures], we'll talk about this in the `Authenticity` section.

Some of the examples given here require that the hash function is a [`cryptographic hash function`] in order to function correctly and securely. In other words, not all hash functions are suitable for cryptographic demands.

Today, the probably most common hash function used, that is also suitable for cryptographic use, is [`SHA2-256`] (and its 512-bit cousin [`SHA2-512`]). The only reason an application would not want to use SHA2-256/512 is because they are vulnerable to [length extension attacks]. However, the revised [`SHA-3`] family fixes that issue, and contains both 256-bit and 512-bit variants (`SHA3-256` and `SHA3-512`, respectively).

[passwords match]: https://en.wikipedia.org/wiki/Cryptographic_hash_function#Password_verification
[digital signatures]: https://en.wikipedia.org/wiki/Digital_signature
[How large is 2^256 by 3Blue1Brown]: https://youtu.be/S9JGmA5_unY
[`checksum`]: https://en.wikipedia.org/wiki/Checksum
[`hash function`]: https://en.wikipedia.org/wiki/Hash_function
[`cryptographic hash function`]: https://en.wikipedia.org/wiki/Cryptographic_hash_function
[`SHA2-256`]: https://en.wikipedia.org/wiki/SHA-2
[`SHA2-512`]: https://en.wikipedia.org/wiki/SHA-2
[length extension attacks]: https://en.wikipedia.org/wiki/Length_extension_attack
[`SHA-3`]: https://en.wikipedia.org/wiki/SHA-3

So in short, in order to know if the `data` you just downloaded is non-corrupt, and you have access to the desired `checksum`, make sure the equation `H(data) = checksum` holds, when `H` is e.g. a hash function in the `SHA-2` or `SHA-3` family. You can find a practical step-by-step guide [here](https://www.maketecheasier.com/verify-md5-sha-1-sha-256-checksum-windows10/).

### Confidentiality
=> Encryption
### Authenticity
=> Signatures
=> Root of Trust (RoT)


[RSA Signing is Not RSA Decryption]: https://www.cs.cornell.edu/courses/cs5430/2015sp/notes/rsa_sign_vs_dec.php

## Considering downloading multiple related files

### Mix-and-match attacks

### Extraneous dependencies attacks

## Considering downloading updates of software

### Fast-forward attacks

### Rollback attacks

