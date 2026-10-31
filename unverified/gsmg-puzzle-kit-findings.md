# Where the puzzle stands: findings and tested nulls (31 October 2026)

A summary of the research kept in [AppleLamps/gsmg-puzzle-kit](https://github.com/AppleLamps/gsmg-puzzle-kit)
(the dossier, log docs 115 to 122, and the full review of 19 October 2026). It lists what decodes,
what is still locked, and what has been tried and failed, so the same ground is not walked twice.

**No new unlock and no private key.** Nothing below opens a locked container.

Tags: **[V]** checked from the bytes in this folder or the kit, **[T]** tested with a planted control
that fired, **[R]** a reading that has not been tested.

## 1. The target and the win test

- The only target is the private key of `1GSMG1JC9wtdSwfwApgj2xcmJPAwx7prBe`, HASH160
  `a9553269572a317e39f0f518cb87c1a0ee1dbae4`. The address has spent, so its public key is exposed.
  The recorded balance was 1.25636967 BTC on 29 September 2026 (the 1.25 BTC principal plus dust).
- `17ucy1K9ZUAaoY6JVtM932W9jUp5LXfyHa` received the two halvings (2.5 BTC on 2020-05-11, 1.25 BTC on
  2024-04-24, both pre-signed with nLockTime at the halving block). It has never spent. It is the
  halving destination, not a puzzle output.
- A correct candidate must be checked against the prize HASH160. Only the **uncompressed** public key
  serialization matches it; the compressed form gives `06bbdc66...` (address `1cc6xayvqpeetixmuXDRsGug7GKyoRdxP`, empty).

## 2. The encryption convention of the solved phases [V]

All three opened containers (phase 2, phase 3, phase 3.2) use the same convention:

```
openssl enc -d -aes-256-cbc -md sha256 -a -in <file> -pass pass:<sha256(answer) as 64 lowercase hex>
```

That is OpenSSL `Salted__`, password = the hex SHA-256 of the answer string, EVP_BytesToKey with
SHA-256 and one iteration, AES-256-CBC. The phase 3.2 plaintext is only 58.9% printable bytes (1,426 of
2,422), so any search that filters for printable output would throw away a correct result.

## 3. What the README lists as "yet to be solved" but is decoded

### Phase 3.2 [V]

- The EBCDIC blob (code page 273, or 1141, which is 273 plus the euro sign; no euro occurs) gives 1,539
  letters. Reciprocal Beaufort with key `THEMATRIXHASYOU` turns them into the Architect's speech from
  *The Matrix Reloaded*, with puzzle edits. `PRIVATEKEY` sits at letter offset 479.
- The 149 digits are a straddling checkerboard (the README calls it VIC). Working key
  `FUBCDORA.LETHINGKYMVPS/JQZXW` with blanks 1 and 4 in the top row ("one for one, four for one").
  Of the 45 possible blank pairs, only {1,4} reproduces the text. The 91 letters are in
  [checkerboard_vic_91.txt](./gsmg-puzzle-kit/checkerboard_vic_91.txt):

  ```
  INCASEYOUMANAGETOCRACKTHISTHEPRIVATEKEYSBELONGTOHALFANDBETTERHALFANDTHEYALSONEEDFUNDSTOLIVE
  ```

- The last object in the phase 3.2 plaintext is a further locked envelope, the **Terminal** (section 4).

### SalPhaseIon textarea [V]

The whole textarea, whitespace removed, is 1,075 characters
([salphaseion-textarea.txt](./gsmg-puzzle-kit/salphaseion-textarea.txt)). Segmented:

| span (0-based) | content | decodes to |
|---|---|---|
| [0,91) | `dbbi...` block | fits the poster's colour program at prime positions (yellow/blue/primes) under a fixed first-23-event mapping; any further role is open |
| [91,195) | a/b run | `matrixsumlist` |
| [195,765) | `faed...` block, 570 letters | no decode found; statistics look like filler, which is not proven |
| [766,829) | a..i/o block | `lastwordsbeforearchichoice` |
| [830,859) | a..i/o block | `thispassword` |
| [860,895) | literal | `shabefourfirsthintisyourlastcommand` |
| [895,959) and [999,1063) | two base64 halves | join into the locked **SalPhaseIon short** envelope |
| [959,999) | a/b run | `enter` |
| [1063,1075) | literal | `shabefanstoo` |

Decode rules: a/b runs are `a`=0, `b`=1, 8-bit ASCII. The a..i/o blocks map `a..i` to digits 1..9 and
`o` to 0, read the whole digit string as **one decimal integer**, and write it as big-endian bytes.
`shabef` reads as `sha` + b(2) + ef(5,6) = `sha256` under A1Z26. The two literals read
"sha256 our first hint is your last command" and "sha256 the answer too"; the second is a reading of the
literal `anstoo`. `matrixsumlist` and `lastwordsbeforearchichoice` look like two operations whose
outputs feed `thispassword`. Their operands are the open problem.

## 4. The three locked containers [V]

All three start `Salted__`. No password is known for any of them. Files are copied by script from the kit,
not retyped.

| container | file | decoded bytes | salt | sha256 of decoded bytes |
|---|---|---:|---|---|
| Terminal (end of phase 3.2) | [terminal.b64](./gsmg-puzzle-kit/terminal.b64) | 96 | `b45a5e3d827593ca` | `291dfd6f3e759ec2e272b35a00c24907da70c3e7a9291b4c13605c7b0b4f3de9` |
| SalPhaseIon short (textarea halves joined) | [salphaseion-short.b64](./gsmg-puzzle-kit/salphaseion-short.b64) | 96 | `3ab585348552415d` | `9e2831e1b34b5f34796df47ccaf6530d48d371c61a6bff84d60db1064fa7a258` |
| Cosmic Duality (second textarea) | [cosmic-duality.b64](./gsmg-puzzle-kit/cosmic-duality.b64) | 1344 | `2d3f6fe06dc950e6` | `b18950551a4dd0cb8a9378f0906ba18c03a15f0ee83eb98c6bc90165c5f79805` |

The Terminal base64 matches this repository's own README at commit `c4b6a20` (April 2020), and the short
envelope matches commit `a7041aa` (May 2021), after removing whitespace and quote markers. `Salted__` and the sizes do not prove AES-CBC for the locked three; under CBC with
PKCS#7 the short ones hold 64 to 79 plaintext bytes and Cosmic Duality 1,312 to 1,327. Which container
opens first, and whether all three must be opened, is not established.

## 5. Tried and failed

Every line here is a null **for the exact configuration tested**: that grammar, those assembly orders,
those password forms and that detector. It is not a proof that the idea is wrong in every form.
Historical counts are as the run logs report them and were not all rerun after the 5 October
detector audit (kit doc 118).

| when | what | size | result | control |
|---|---|---|---|---|
| to 25 Sep | Corpus combinations against the containers, poster "sum lists" in 17 encodings crossed with last-words pools, dbbi with `b` as zero, Architect windows, halves at string level (kit doc 115) | 7.29 billion decrypts | null | planted |
| 3 Oct | The doc 115 gaps: second password order, raw and double-hash forms, scripted pools (kit doc 116) | 26.8 billion decrypts, 195.7 million scalars through the win test | valid pads at expectation; 1,940 flags, all noise | planted |
| 3 Oct | Riddle rounds 1 to 5: each label worked as a riddle with one answer, then every answer under 14 ciphers and EVP md5/sha1/sha256/sha512 and PBKDF2-SHA256 10k (kit doc 117) | small | null | planted |
| 15 Oct | faed full-period Bifid with square `dbifhcegaklmnopqrstuvwxyz` gives the header `btcseed`; nothing past the header beats a header-preserving shuffle; `btcseed` as a password null (kit doc 120) | | header only | shuffle nulls |
| 17 Oct | Arithmetic: faed's last 32 letters hold no `g` and no `e`, and 10^32 is divisible by 2^32, so the low 4 bytes of the whole-block decimal decode are fixed and non-printable for every `g` or `e` zero mask. This closes the 2^107 "arbitrary g as zero" case **for that decode only** (kit doc 121) | proof | closed for that decode | |
| 17 Oct | Neo screen lines (`wakeupneo`, `thematrixhasyou`, `followthewhiterabbit`, `knockknockneo`) in their variants, and `theseedisplanted`, against all three containers | 596 + 83 candidates, 14,328 tests for the Neo lines | null | planted fired |
| 19 Oct | faed single-letter deletion (108 cases) and delete-X plus zero-Y (720 cases), whole-block decode | 828 cases | 0 text solutions | planted fired |
| 19 Oct | faed as 7/12/19-digit chunks, 9x9 Polybius pairs, trit regroup over all 9! labelings | | inside shuffle bands | planted fired |
| 19 Oct | Poster sums with dbbi colour numbers (blue `b`=2, yellow `be`=25) | 6,239 candidates, 299,472 decrypts | 1,211 pads vs about 1,174 expected, 0 flags | planted fired |
| 19 Oct | Pair ledger block (a): 600 poster-camp x film-camp strings | 28,800 decrypts | 108 pads vs 112.9 expected, 0 flags | planted fired |
| 19 Oct | Pair ledger block (b): 16 riddle answers for `matrixsumlist` x 175 Architect windows, 4 assemblies, both cases | 22,765 candidates, 1,092,720 decrypts | 4,280 pads vs 4,285.2 expected, 0 flags | planted fired |
| 19 Oct | The 1 April 2021 hint `{1},{4},{21}` as a selection template over every puzzle list, plus book-cipher reads | 1,912 candidates, 91,776 decrypts | 355 pads vs 359.9 expected, 0 flags | planted fired |

"Valid pads" are decrypts whose last block happens to be valid PKCS#7 padding. About 1 in 256 wrong
passwords gives one by chance, so a count at expectation is what a null looks like. A "flag" is a
decrypt the structure recogniser marks for a human look.

Other checks with nothing found: the poster PNG (no hidden data, QR clean at codeword level), the
textarea whitespace (one 0x20 after each character, no channel), the off-white `#FEFEFE` cell (it is
symbol 21 of the dbbi colour program), XOR and interleave of the two 80-byte containers.

## 6. What is still open

- The operands of `matrixsumlist` and `lastwordsbeforearchichoice`. This is the main open problem.
- What "our first hint is your last command" and "the answer too" point to.
- The purpose of faed and of the dbbi leftovers.
- Unexplained details: the four centre cells (`0000`), the two leftover colour-program symbols, the
  trailing `O` of `CIAOBELLAO` in the Architect text, the doubled `SELF`, "as wide as the first one seen"
  in the checkerboard riddle, and the minus sign in the phase 2 coordinate step.
- Untested readings [R]: `{1},{4},{21}` as checkerboard blanks 1 and 4 plus colour symbol 21; "first
  hint" and "last command" as ASCII NUL (0) and DEL (127).

## 7. How to reproduce

The kit's `tools/` folder builds the harness (`h3.c` decrypt tester, `wintest.py`, `plant.py` for
planted controls, `verify.py` for the 60 dossier checks). Run a planted control before trusting any null.
Do not submit guesses to `gsmg.io/phase1verification`; it only gates stage 1.
