# Where the puzzle stands: findings and tested nulls (1 November 2026)

A summary of the research kept in [AppleLamps/gsmg-puzzle-kit](https://github.com/AppleLamps/gsmg-puzzle-kit)
(the dossier, log docs 115 to 122, and the full review of 19 October 2026), updated on 1 November 2026
with the other research repositories collected in [AppleLamps/combined-puzzle](https://github.com/AppleLamps/combined-puzzle)
(puzle, GSMG-CLEAN, gsmg, gsmg-1.2, gsmg-1.2-2, gsmg-haiku, grok-gsmg-puzzle, 5g-puzzle and a September fork of
this repository, each as of 21 October 2026). It lists what decodes, what is still locked, and what has been
tried and failed, so the same ground is not walked twice.

**No new unlock and no private key.** Nothing below opens a locked container to readable output. Ten
research repositories rescanned every stored output for a prize key on 21 October 2026 (more than 23 million
candidate keys in total, against both addresses under both public key forms): no match.

Tags: **[V]** checked from the bytes in this folder or the kit, **[T]** tested with a planted control
that fired, **[R]** a reading that has not been tested.

## 1. The target and the win test

- The main target is the private key of `1GSMG1JC9wtdSwfwApgj2xcmJPAwx7prBe` ("Half"), HASH160
  `a9553269572a317e39f0f518cb87c1a0ee1dbae4`. The address has spent, so its public key is exposed.
  The balance was 1.25649674 BTC on 1 November 2026 (the 1.25 BTC principal plus dust).
- `17ucy1K9ZUAaoY6JVtM932W9jUp5LXfyHa` ("Better Half") received the two halvings: 2.5 BTC in
  transaction `2aa9a4a9...` (block 630,001, nLockTime 629,998) and 1.25 BTC in `88cdb3cd...`
  (block 840,725 on 2024-04-24, nLockTime 840,003) [V]. These locktimes are a few blocks off the halvings,
  which is what wallet software sets by default, so the chain does not show the transfers were pre-signed.
  It holds 3.75055856 BTC and has never spent, so only its HASH160 is known. Whether it is a prize is not
  established, but the phase 3.2 message says "the private keys belong to half and better half", so gate
  every candidate against **both** addresses.
- Only the **uncompressed** public key serialization matches Half's HASH160; the compressed form gives
  `06bbdc66...` (address `1cc6xayvqpeetixmuXDRsGug7GKyoRdxP`, empty). The 2021 "neighbors" payment (section 1a)
  also uses the uncompressed form. For Better Half both forms are possible.
- [tools/prize_gate.py](../tools/prize_gate.py) does this: both addresses, both forms, and keys written as raw
  bytes, hex, WIF, mini key, base64 or decimal anywhere in a decrypted file. Its selftest plants every
  encoding in both slots (55 checks). An older gate in several repositories checked Half only, or only
  printed decrypts with 3 or more padding bytes; a correct 79-byte plaintext in an 80-byte envelope has
  exactly 1.

## 1a. On-chain messages [V]

`3GSMG24TujqfMJG1kQoBX18DzJHQLeJYMK` paid small amounts with `OP_RETURN` messages to the compressed-key
addresses of sha256(answer) for the solved answers (table in the
[README](../README.md#on-chain-messages-from-the-puzzle)): six `GSMG.io:` checkpoints on 2020-03-24, two
`Good job, Neo!` on 2020-04-03 to the URL `gsmg.io/theseedisplanted` read as a key and its bits reversed,
`Halving` in block 630,001, and `GSMG.io neighbors, half and double` on 2021-07-18 to the uncompressed
addresses of P+G, P-G, 2P and P/2. All addresses re-derived and all messages read from the chain on
1 November 2026. The halving transaction signed by the prize key spends output 1 (700 sat) of the
`Halving` transaction, and they are transactions 230 and 231 of block 630,001, so the sender is tied to the
prize key holder. The checkpoints confirm known answers only. Messages from 2025 on ("From Neo",
"BULLSHIT", "Neo wallet ...", "Yes") come from other senders, often the checkpoint addresses themselves,
whose keys are public; they are not creator messages. One unlabelled 2020-04-07 payment, to
`1NULY7DhzuNvSDtPkFzNo6oRTZQWBqXNE9`, is not identified.

A separate run of vanity-address messages in May 2026 from `1GSMG9VDL...` (`leavethematrix`,
`yourlastcommand`, `hereismysecret`, `isolveditwithanabacus`, `secondanswer`, `GSMGJH`, `GSMGBH`, `WITNESS`)
has no tie to the prize key. A vanity prefix authenticates nothing.

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

A poster observation points into the Architect text: give the first 24 primes to the 24
coloured cells in spiral order and blue sums to 484, yellow to 479. The difference, 5, is a blue prime, and
"zeroing" it (the 2021-12-26 hint) leaves 479, the letter offset of `PRIVATEKEY` in the Architect text
(it begins `PRIVATEKEYYOUVEEARNEDIT`). `PRIVATEKEY` also occurs at offset 1238. This depends on the
letters-only, 0-based convention, and the colours are fixed by the URL bits, so it points to a place in the
text and nothing more. The text at 479 tested as an answer (476 candidates): null.

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

More on `dbbi` [V]: if every prime-numbered cell must be `b` or `be` and every other cell is one letter,
the 91 letters parse in exactly two ways: 84 cells (23 prime cells, 16 `b` and 7 `be`) or 83 cells
(15 `b`, 8 `be`). No letter-preserving shuffle of 20,000 tried parses at all. The earlier "fits the colour
program" result uses one of these; picking between them needs a further rule.

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
opens first, and whether all three must be opened, is not established. "No password is known" means no
password that gives readable output.

The creator confirmed on 2023-06-10 (#8569) that phase 3.2 "is not totally solved, as the final block
hasn't been decrypted" ("Correct."), and denied that the SalPhaseIon hint is inside it ("No."). A bare WIF
(51 or 52 characters) would encrypt to 64 bytes, not 80, so the Terminal and the short envelope do not hold
a bare WIF; a 64-character hex key would give a full block of padding.

### Padding-only unlocks

Several passwords shared in the Telegram group "open" the envelopes. Each uses the old MD5 key derivation,
not the convention above, and each ends in a single `0x01` padding byte, which about 1 wrong password in 256
gives by chance. None is readable. Reproduced from the files in this folder:

| envelope | password | output | sha256 of output |
|---|---|---:|---|
| SalPhaseIon short | `matrixsumlistenterlastwordsbeforearchichoicethispasswordmatrixsumlist` | 79 bytes | `1449a2178eea7c0e...88c626bf` |
| Cosmic Duality | the 32 raw bytes `a795de11...52e50735`, the XOR of sha256 of `matrixsumlist`, `enter`, `lastwordsbeforearchichoice`, `thispassword`, `matrixsumlist`, `yourlastcommand`, `secondanswer` (the two `matrixsumlist` cancel) | 1,327 bytes | `4f7a1e4efe4bf6c5...a5e9c081` |

The Cosmic Duality output has 7.87 bits per byte of entropy and grows under zlib (1,338 bytes). It has been
promoted since 9 August 2025 as "correctly decrypted ... does not contain cleartext by design". Two
repositories in the collection called it an unlock; they were wrong. A further chain built on the short
envelope's output (its first 32 bytes as a WIF opening the Terminal to 79 bytes, then a fitted XOR mask on
the Cosmic output) gives more padding-level events and no text. The Terminal and the short envelope are
not independent routes there: the second step uses the first step's output.

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
| 15 Oct | faed full-period Bifid with square `dbifhcegaklmnopqrstuvwxyz` gives the header `btcseed` (first posted in the Telegram group on 2025-06-12, #43248); nothing past the header beats a header-preserving shuffle; `btcseed` as a password null (kit doc 120) | | header only | shuffle nulls |
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

Doc numbers in the rows above follow the kit as read on 31 October. In the 21 October snapshot kept in
combined-puzzle, doc 120 is the full-padding-gate run in the next table.

### From the other repositories in combined-puzzle

| when | where | what | size | result | control |
|---|---|---|---|---|---|
| 6 to 7 Aug | puzle | Phrase combinations from every label and hint | 386,794 passwords, 3,094,352 decrypts | 12,132 pads (0.39%, chance), 0 readable | phase 3.2 opens |
| 6 to 7 Aug | puzle | Shared base-9 substitution for dbbi and faed (all 9! maps), split envelopes, 27 OpenSSL ciphers, PBKDF2 1k and 10k, 23/16/7 endgame, 479-anchored selections, a "passport date" family | 362,880 maps; 4,997,120 gated keys for the passport family; smaller families of 3,240 to 13,248 | null | planted key and phase 3.2 |
| 8 Sep | 5g-puzzle | 4 key derivations x 3 envelopes over the corpus | 4,776 | 25 pads, chance | self-test |
| 13 to 14 Sep | GSMG-CLEAN | `bg` split of dbbi into 64 hex-like tokens, checked as a digest against 16.8 million harvested strings | 1.117 billion checks | 0 | 8 of 8 planted |
| 13 to 14 Sep | GSMG-CLEAN | Seven-key Bifid outputs as passwords | 1,079,568 decrypts | 28 pads vs 25 expected | 200 shuffles |
| 13 to 14 Sep | GSMG-CLEAN | `matrixsumlist` pipeline: 552 sum lists, 4,677 outputs; last-words referents 15,676 strings; "zeroed" envelope variants 333,670 decrypts | | null | shuffles and planted |
| 13 to 14 Sep | GSMG-CLEAN | faed recovery: lossy 2x2 Hill (2,519,424 constructions), source-passage Hill keys (245,184), Architect words as keys (273,478), checkerboard windows (671,349) | | null | planted message recovered exactly |
| 26 to 27 Sep | gsmg | Zero insertion at primes, whole objects as passwords, the film's other "choice" lines; PBKDF2 tier B (737,984 decrypts, 3,000 pads vs 2,883); all 106 OpenSSL ciphers (767,440 decrypts); single-character base64 corruption (about 1.27 million decrypts); Hill 3x3 with 152 poster keys | | null | planted |
| 27 Sep | gsmg-1.2-2 | Records 135 to 141: SELECT anchor, Architect and faed sums, label permutations, "last command = reverse" | 2,729 candidates, about 32,700 decrypts | all pad 1 | yes |
| to 15 Oct | gsmg-haiku | All 300,000 invertible 2x2 Hill matrices mod 25 on the Bifid output; the four singular mod-26 matrices fitting `FEXM`->`GSGQ` (contradicted by 63 to 100 digraphs with no preimage); 3x3 Hill to `IFINDOUBT` (impossible by a mod-5 invariant) | | null or proof | forward control |
| to 15 Oct | gsmg-haiku | Bifid row-bit stream as text or keys (1,440 models, 82,704 keys); 64- or 63-byte seed through 295 BIP32 paths; faed digits as gaps in the Architect text | | null | BIP32 test vectors; planted |
| 17 to 21 Oct | grok-gsmg-puzzle | 18 batteries on the locked envelopes, rerun after a detector audit | 1,763,105 decrypts | 6,886 pads vs 6,914 expected, 0 flags | phase 3.2 fires |
| 21 Oct | gsmg-puzzle-kit doc 120 | Terminal and short envelope, 753 preregistered strings x 17 forms (EVP-SHA256, EVP-MD5, PBKDF2 10k), every pad decrypted in full | 25,602 | 97 pads vs 100.4 expected, all pad 1 | 3 planted envelopes |
| 21 Oct | all ten | Prize-gate rescan of every stored output (puzle 15.87M keys, GSMG-CLEAN 7.34M, grok 9,393, kit 94,046, others smaller) | over 23 million keys | 0 | 55-check selftest |

Two cautions on older nulls. Before 5 October, several detectors treated the phase 3.2 plaintext as
"opaque" (it is only 58.9% printable) and only printed outputs with 3 or more padding bytes, so a correct
result with 1 or 2 padding bytes could have been missed. The grok batteries and kit doc 120 were rerun with
that fixed; most earlier rows were not. Many pre-September campaigns also used the MD5 key derivation, or
checked Half only, or loaded the Terminal truncated to 48 bytes; GSMG-CLEAN's `04_DEAD_ENDS_TESTED.md`
marks those as void.

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

### Readings that are not tested or not confirmed

- [R] `{1},{4},{21}` (the 2021-04-01 hint) as checkerboard blanks 1 and 4 plus colour symbol 21.
- [V, meaning R] `dbbi` (a=0) minus the checkerboard message (A=0), mod 26, letter by letter, gives
  `VOZIJBDTIQBRGVEOMZNBCYOUWONXCPKW...`. `YOUWON` starts at 0-based index 21, and the letters at 1-based
  positions 1, 4 and 21 are `V`, `I`, `C`. The tail is 64 letters over 24 distinct letters, so it is not a
  hex digest. One write-up puts the chance of its supporting alignments at 8.4%. On 2026-09-01, about five
  hours after a solver posted this together with an Executive Order 13224 reading of `enter`, the creator
  wrote "Pfff. Coincidence." (#70307), not as a reply.
- [R] "first hint" and "last command" as ASCII NUL (0) and DEL (127). The creator said on 2024-11-29 "I
  think I'll be going for ASCII 127 myself" (#32613) in a joke exchange. The first thing the creator posted
  in the group about the puzzle was the SHA-256 of the phase 1 password (#225, 2019-04-22).
- [R] `HILLFEXMGSGQ`: on the 84-cell `dbbi` parse with prime `b` = minus its position, prime `be` = plus its
  position and other letters a..i = 1..9, laid out 7x12, the column sums mod 26 spell `HILLFEXMGSGQ`. Using
  `FEXM`->`GSGQ` as a 2x2 Hill example on the Bifid output gives `IFINDO` and then noise. The sign rule,
  grid shape and modulus are choices; the 6x14 shape gives nothing.
- [R] The `#FEFEFE` cell: under the 84-cell model the yellow and blue prime sums are 317 and 557, and pixel
  (317, 557) of the poster falls inside the off-white cell. A fit found after the fact.
- [R] faed may not be one homogeneous block: a 4-part G-test gives p = 0.0018 with cuts near 220, 435 and 540
  (gsmg doc 118). Not re-verified.
- Creator statements bearing on the target, all from Telegram (see the README timeline): the key is a
  "Regular Bitcoin Private key" (#20223); "If wallet != empty, puzzle not solved" (#32535); yinyang "is the
  next phase" and "when yingyang is reached, 2 hours max" (#39237, #39224); "If any of you reaches the next
  phase, the price is taken in no-time" (#60314); SalPhaseIon is "100% solveable": "Yes" (#66588); the
  5 BTC "was never the actual prize" (#66593). None of these can be checked.

## 7. How to reproduce

The kit's `tools/` folder builds the harness (`h3.c` decrypt tester, `wintest.py`, `plant.py` for
planted controls, `verify.py` for the 60 dossier checks). Run a planted control before trusting any null.
Gate every candidate key with [tools/prize_gate.py](../tools/prize_gate.py). Do not submit guesses to
`gsmg.io/phase1verification`; it only gates stage 1.

If you copy plaintexts from combined-puzzle, regenerate them from the archived pages
([archive/pages/](../archive/pages/)): the `data/phase*_plaintext.bin` files in its GSMG-CLEAN copy lost their
carriage returns on import (642, 4,032 and 2,411 bytes instead of 648, 4,090 and 2,422) and no longer match
their checksums. Do not copy the Telegram exports wholesale; they hold private conversation. Quote the
message ids instead.
