---
description: Simple tests
---

# LAB: Hashcat



> hashcat -m 500 -a 0 hash.txt rockyou.txt

hashcat (v6.2.6) starting

Successfully initialized the NVIDIA main driver CUDA runtime library.

Failed to initialize NVIDIA RTC library.

* Device #1: CUDA SDK Toolkit not installed or incorrectly installed. CUDA SDK Toolkit required for proper device support and utilization. Falling back to OpenCL runtime.
* Device #1: WARNING! Kernel exec timeout is not disabled. This may cause "CL\_OUT\_OF\_RESOURCES" or related errors. To disable the timeout, see: https://hashcat.net/q/timeoutpatch OpenCL API (OpenCL 3.0 CUDA 12.2.146) - Platform #1 \[NVIDIA Corporation] ========================================================================
* Device #1: NVIDIA GeForce RTX 4060 Laptop GPU, 8064/8187 MB (2046 MB allocatable), 24MCU

## OpenCL API (OpenCL 3.0 ) - Platform #2 \[Intel(R) Corporation]

* Device #2: Intel(R) RaptorLake-S Mobile Graphics Controller, 7360/14811 MB (2047 MB allocatable), 16MCU

Minimum password length supported by kernel: 0 Maximum password length supported by kernel: 256

Counting lines in hash.txt. Please be patient...Counted lines in hash.txtHashfile 'hash.txt' on line 1 (5f4dcc3b5aa765d61d8327deb882cf99): Separator unmatched Hashfile 'hash.txt' on line 2 (098f6bcd4621d373cade4e832627b4f6): Separator unmatched Hashfile 'hash.txt' on line 3 (d8578edf8458ce06fbc5bb76a58c5ca4): Separator unmatched Parsing Hashes: 1/12 (8.33%)...Hashfile 'hash.txt' on line 7 ($2b$12...OD3RCH.pCJBOOEICXau0hLmwYiERQIXy): Token length exception Hashfile 'hash.txt' on line 8 ($2b$12...ew9W2ASBSZFOSRj8QqfFrvKiWEuZs8i6): Token length exception Hashfile 'hash.txt' on line 9 ($2b$12....zmENTjEhjI3UoFAAlt6Ra1Pv9/6OTeq): Token length exception Hashfile 'hash.txt' on line 10 (a9993e364706816aba3e25717850c26c9cd0d89d): Separator unmatched Hashfile 'hash.txt' on line 11 (7c4a8d09ca3762af61e59520943dc26494f8941b): Separator unmatched Hashfile 'hash.txt' on line 12 (e5e9fa1ba31ecd1ae84f75caaa474f3a663f05f4): Separator unmatched Parsing Hashes: 3/12 (25.00%)...Sorting hashes. Please be patient...Sorted hashes

* Token length exception: 3/6 hashes This error happens if the wrong hash type is specified, if the hashes are malformed, or if input is otherwise not as expected (for example, if the --username option is used but no username is present)

Removing duplicate hashes. Please be patient...Removed duplicate hashesSorting salts. Please be patient...Sorted saltsComparing hashes with potfile entries. Please be patient...Compared hashes with potfile entriesGenerating bitmap tables...Generated bitmap tablesHashes: 3 digests; 3 unique digests, 1 unique salts Bitmaps: 16 bits, 65536 entries, 0x0000ffff mask, 262144 bytes, 5/13 rotates Rules: 1

Optimizers applied:

* Zero-Byte
* Single-Salt

ATTENTION! Pure (unoptimized) backend kernels selected. Pure kernels can crack longer passwords, but drastically reduce performance. If you want to switch to optimized kernels, append -O to your commandline. See the above message to find out about the exact limits.

Watchdog: Temperature abort trigger set to 90c

Initializing device kernels and memory. Please be patient...Initializing backend runtime for device #1. Please be patient...Initialized backend runtime for device #1Initializing backend runtime for device #2. Please be patient...Initialized backend runtime for device #2Host memory required for this attack: 2950 MB

Initialized device kernels and memoryStarting self-test. Please be patient...Finished self-testDictionary cache hit:

* Filename..: rockyou.txt
* Passwords.: 14344384
* Bytes.....: 139921497
* Keyspace..: 14344384

Starting autotune. Please be patient...Finished autotune

\[s]tatus \[p]ause \[b]ypass \[c]heckpoint \[f]inish \[q]uit =>

Cracking performance lower than expected?

* Append -O to the commandline. This lowers the maximum supported password/salt length (usually down to 32).
* Append -w 3 to the commandline. This can cause your screen to lag.
* Append -S to the commandline. This has a drastic speed impact but can be better for specific attacks. Typical scenarios are a small wordlist but a large ruleset.
* Update your backend API runtime / driver the right way: https://hashcat.net/faq/wrongdriver
* Create more work items to make use of your parallelization power: https://hashcat.net/faq/morework

\[s]tatus \[p]ause \[b]ypass \[c]heckpoint \[f]inish \[q]uit =>

$1$salt1234$Vi7QMXxcGTN/X20uk4Vwl.:monkey \[s]tatus \[p]ause \[b]ypass \[c]heckpoint \[f]inish \[q]uit =>

$1$salt1234$my9KtjNgeZMY6V77juF7X1:letmein \[s]tatus \[p]ause \[b]ypass \[c]heckpoint \[f]inish \[q]uit =>

$1$salt1234$J.e6yQS5jB8kyBBkCDbkX/:admin

Session..........: hashcat Status...........: Cracked Hash.Mode........: 500 (md5crypt, MD5 (Unix), Cisco-IOS $1$ (MD5)) Hash.Target......: hash.txt Time.Started.....: Tue Jul 22 13:31:05 2025 (14 secs) Time.Estimated...: Tue Jul 22 13:31:19 2025 (0 secs) Kernel.Feature...: Pure Kernel Guess.Base.......: File (rockyou.txt) Guess.Queue......: 1/1 (100.00%) Speed.#1.........: 58832 H/s (5.60ms) @ Accel:2 Loops:125 Thr:256 Vec:1 Speed.#2.........: 4760 H/s (12.17ms) @ Accel:256 Loops:1 Thr:16 Vec:1 Speed.#\*.........: 63592 H/s Recovered........: 3/3 (100.00%) Digests (total), 3/3 (100.00%) Digests (new) Progress.........: 864256/14344384 (6.03%) Rejected.........: 0/864256 (0.00%) Restore.Point....: 0/14344384 (0.00%) Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:875-1000 Restore.Sub.#2...: Salt:0 Amplifier:0-1 Iteration:999-1000 Candidate.Engine.: Device Generator Candidates.#1....: momo4ever -> marwane Candidates.#2....: 123456 -> ryanscott Hardware.Mon.#1..: Temp: 51c Util: 0% Core: 600MHz Mem: 810MHz Bus:8 Hardware.Mon.#2..: N/A

Started: Tue Jul 22 13:30:33 2025 Stopped: Tue Jul 22 13:31:21 2025

***

Example:

$1$salt1234$J.e6yQS5jB8kyBBkCDbkX/&#x20;

MD5-Crypt używający soli: salt1234

atak słownikowy: > hashcat -m 500 -a 0 hash.txt rockupu.txt --show

atak maską (brute force): **> hashcat -m 500 -a 3 hash.txt ?l?l?l?l?l?l?l?l**

-m 500  -> tryb MD5-Crypt

-a 0 -> atak słownikowy

-a 3 -> atak brute-force

?l - mała litera, ?d - cyfra

\--show -> pokazuje wynik

\--force - gdy hashcat zgłasza błąd sprzetowy (CPU)

