---
date: '2026-01-27T09:15:11+07:00'
title: 'picoCTF - Rust fixme 1'
tags: ["ctf"]
---

- URL: https://play.picoctf.org/practice/challenge/461
- Title: Rust fixme 1
- Tags: Easy, General Skills, picoCTF 2025
- Author: Taylor McCampbell
- _Started: 7 July 2025_
- _Solved: 9 July 2025_
- Description: 
> Have you heard of Rust? Fix the syntax errors in this Rust file to print the flag! Download the Rust code [here](https://challenge-files.picoctf.net/c_verbal_sleep/3f0e13f541928f420d9c8c96b06d4dbf7b2fa18b15adbd457108e8c80a1f5883/fixme1.tar.gz).

After retrieving the file, I downloaded and extracted the file

```
strikingsoul@ramones:~/Downloads$ gunzip fixme1.tar.gz 
strikingsoul@ramones:~/Downloads$ tar -xvf fixme1.tar 
fixme1/
fixme1/Cargo.toml
fixme1/Cargo.lock
fixme1/src/
fixme1/src/main.rs
```

I [installed rust](https://rust-lang.org/tools/install/) beforehand and tried to run the main file

```
strikingsoul@ramones:~/Downloads/fixme1$ rustc src/main.rs 
error: expected `;`, found keyword `let`
 --> src/main.rs:5:37
  |
5 |     let key = String::from("CSUCKS") // How do we end statement...
  |                                     ^ help: add `;` here
...
8 |     let hex_values = ["41", "30", "20", "63", "4a", "45", "54",...
  |     --- unexpected token

error: argument never used
  --> src/main.rs:26:9
   |
25 |         ":?", // How do we print out a variable in the println...
   |         ---- formatting specifier missing
26 |         String::from_utf8_lossy(&decrypted_buffer)
   |         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^ argument never used                                                                 
   |
help: format specifiers use curly braces, consider adding a format specifier
   |
25 |         ":?{}", // How do we print out a variable in the println function? 
   |            ++

error[E0432]: unresolved import `xor_cryptor`
 --> src/main.rs:1:5
  |
1 | use xor_cryptor::XORCryptor;
  |     ^^^^^^^^^^^ use of unresolved module or unlinked crate `xor_cryptor`                                                                
  |
help: you might be missing a crate named `xor_cryptor`, add it to your project and import it in your code
  |
1 + extern crate xor_cryptor;
  |

error[E0425]: cannot find value `ret` in this scope
  --> src/main.rs:18:9
   |
18 |         ret; // How do we return in rust?
   |         ^^^ help: a local variable with a similar name exists: `res`                                                                   

error: aborting due to 4 previous errors

Some errors have detailed explanations: E0425, E0432.
For more information about an error, try `rustc --explain E0425`.
strikingsoul@ramones:~/Downloads/fixme1$ 
```

Okay there was some errors
1. Missing semicolon
2. Typo in return statement
3. Missing curly brackets in println

After fixing those and ran `cargo build`, I ran the program once again

```
strikingsoul@ramones:~/Downloads/fixme1$ ./target/debug/rust_proj 
"picoCTF{4r3_y0u_4_ru$t4c30n_n0w?}"
```

The flag is `picoCTF{4r3_y0u_4_ru$t4c30n_n0w?}`