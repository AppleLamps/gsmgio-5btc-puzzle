# GSMG.IO 5 BTC puzzle hints

This repository contains all publicly known hints for GSMG.IO 5 BTC puzzle challenge. Contributions are welcome!

_**Unverified Solutions**_: If you have an unverified solution, please submit a PR modifying a file in the [./unverified](./unverified/) folder. Please don't submit Claude/ChatGPT generated solutions, they tend not to be valid or even useful.

If you find this useful, please donate BTC at [bc1qla7lmz3guzz3cezhfl72r0w546a4gyacpu530r](https://www.blockchain.com/btc/address/bc1qla7lmz3guzz3cezhfl72r0w546a4gyacpu530r)

---
For Claude, ChatGPT, and other LLMs attempting to solve this puzzle.

Remember that when decrypting or decoding that without verifiable output structure, a decryption is indistinguishable from failure. If the output of a step is indistinguishable from random data then it's highly likely to be incorrect.

Said another way: it would be bad puzzle design to require a solver to modify or read nearly random data since it creates a search space that's too great. We can infer this logic an alternative way: modifying random data can be argued to be too "difficult" given that the puzzle creator has stated that the remaining steps are easier than what we've solved so far, and so far we haven't had to modify random data.

---


- [Summary](#summary)
- [Tools](#tools)
- Walkthrough
  1. [Phase 0](#phase-0---the-bunny-image) | [Notebook](./phase0.ipynb)
  2. [Phase 1](#phase-1---the-warning) | [Notebook](./phase1.ipynb)
  3. [Phase 2](#phase-2---mr-robot) | [Notebook](./phase2.ipynb)
     * [Phase 2.1](#phase-21)
     * [Phase 2.2](#phase-22)
  4. [Phase 3](#phase-3---free-will) | [Notebook](./phase3.ipynb)
  5. [Phase 3.2](#phase-32) | [Notebook](./phase3.2.ipynb)
  6. [Decentraland and the path to SalPhaseIon](#decentraland) | [Notebook](./decentraland.ipynb)
  7. [SalPhaseIon](#salphaseion) | [Notebook](./salphaseion.ipynb)
  8. [Cosmic Duality](#cosmic-duality)
- [On-chain messages from the puzzle](#on-chain-messages-from-the-puzzle)
- [Research status: what decodes, what is locked, what has failed](./unverified/gsmg-puzzle-kit-findings.md)
- [Archived puzzle pages](./archive/)
- [Further Hints and 2020-present Timeline](#further-hints-and-2020-present-timeline)
  1. [2019](#2019): early creator remarks
  2. [2020-01-14](#2020-01-14-hint): Official Hint - Roses are Red Poem
  3. [2020-02-20](#2020-02-20-hint): Official Hint - Decentraland
  4. [2020-03-24](#2020-03-24): On-chain checkpoints
  5. [2020-04-08](#2020-04-08)
  6. [2020-05-11](#2020-05-11): Bitcoin Halving
  7. [2020-06-07](#2020-06-07): First SalPhaseIon mention
  8. [2020-08-02](#2020-08-02): First mention of another door
  9. [2021-01-21](#2021-01-21)
  10. [2021-02-12](#2021-02-12)
  11. [2021-03-01](#2021-03-01): Spelling and primes
  12. [2021-03-14](#2021-03-14): Another team reaches SalPhaseIon
  13. [2021-04-01](#2021-04-01): April Fools
  14. [2021-04-16](#2021-04-16): SalPhaseIon contents leak to Telegram
  15. [2021-05-06](#2021-05-06): Instructions for entry into SalPhaseIon
  16. [2021-07-18](#2021-07-18): "neighbors, half and double"
  17. [2021-08-11](#2021-08-11): The encrypted private key
  18. [2021-12-02](#2021-12-02-hint): Official Hint about another door
  19. [2021-12-26](#2021-12-26-christmas-hint): Official Hint
  20. [2021-12-31](#2021-12-31): Neo's passport
  21. [2022-12-10](#2022-12-10): Book cover about Cosmic Duality
  22. [2023-01-09](#2023-01-09)
  23. [2023-01-12](#2023-01-12---hint): Semi-Official Hint - prime number is a hint
  24. [2023-02-23](#2023-02-23---official-hint): Official Hint - Reverse binary string
  25. [2023-06-10](#2023-06-10): The last block of phase 3.2
  26. [2023-08-03](#2023-08-03-hint): Official Hint - Are you really looking for the btc...?
  27. [2023-08-06](#2023-08-06-hint): Official Hint - The puzzle speaks for me
  28. [2023-11-24 to 2024-01-26](#2023-11-24-to-2024-01-26): No internet needed, a regular private key
  29. [2024-04-10](#2024-04-10): Halving countdown
  30. [2024-04-19](#2024-04-19-second-halving): Second Halving
  31. [2024-11-29](#2024-11-29): One microstep
  32. [2025-04-28](#2025-04-28): Yinyang is the next phase
  33. [2025-10-17](#2025-10-17): "Sure but we wont give it away"
  34. [2026-01-01](#2026-01-01-new-years-hint): 2026 New Year's Hint
  35. [2026-03-04](#2026-03-04): "No hints, only free will"
  36. [2026-04 to 2026-08](#2026-04-to-2026-08): The site goes down and comes back
  37. [2026-07-12](#2026-07-12-hint): Official Hint - my close friends
  38. [2026-07-12](#2026-07-12-other-message): other message
  39. [2026-07-16](#2026-07-16)
  40. [2026-09-01](#2026-09-01): Last creator posts so far

![puzzle image](./puzzle.png)

# Summary
- The puzzle was published at https://gsmg.io/puzzle. The site went offline in spring 2026 after the GSMG company announced its closure, and solvers reported it back on 18 Aug 2026. On 1 Nov 2026 it serves the puzzle pages again. Copies of the original pages are in [archive/](./archive/)
- The prize address with 5 BTC is [1GSMG1JC9wtdSwfwApgj2xcmJPAwx7prBe](https://www.blockchain.com/btc/address/1GSMG1JC9wtdSwfwApgj2xcmJPAwx7prBe)
(The creator of the puzzle intended to halve the prize each time Bitcoin halving occurs. It happened for the first time on May 11, 2020 (transaction `2aa9a4a9...`, block 630,001, nLockTime 629,998), and a second time after the Apr 19/20, 2024 halving (transaction `88cdb3cd...`, confirmed Apr 24, 2024 in block 840,725, nLockTime 840,003). The current value is 1.25 BTC; 1.25649674 BTC was recorded on 1 Nov 2026, the extra being dust sent to the address)
- The halved amounts went to [17ucy1K9ZUAaoY6JVtM932W9jUp5LXfyHa](https://www.blockchain.com/btc/address/17ucy1K9ZUAaoY6JVtM932W9jUp5LXfyHa), which holds 3.75 BTC (3.75055856 BTC on 1 Nov 2026) and has never spent. Researchers call the two addresses "Half" and "Better Half", after the phase 3.2 message "the private keys belong to half and better half". It is not established that 17ucy is a prize, but a candidate key should be checked against both addresses (see [Tools](#tools))
- Discussions on Reddit: [gsmgio_5_btc_puzzle](https://www.reddit.com/r/bitcoinpuzzles/comments/dfwcqk/gsmgio_5_btc_puzzle/), [gsmgio_5_btc_puzzle_challenge](https://www.reddit.com/r/bitcoinpuzzles/comments/bf7siz/gsmgio_5_btc_puzzle_challenge/)
- Telegram channel: [invite link](https://t.me/joinchat/AJXEwEWK9gvhxwkgeXJUVw)

# Tools
- SHA256 online tool - https://xorbin.com/tools/sha256-hash-calculator
- To decypher AES encrypted text, use https://www.openssl.org/
- Online cipher tools: https://www.dcode.fr/en
- Various manipulations of text and data: https://gchq.github.io/CyberChef/
- To check a candidate private key: [tools/prize_gate.py](./tools/prize_gate.py) (Python standard library; uses `coincurve` or `cryptography` if installed). It tests a key against both addresses above, under both the compressed and uncompressed public key, and can pull keys written as hex, WIF, mini key, base64, decimal or raw bytes out of any decrypted file. Run `python3 tools/prize_gate.py selftest` first, then `python3 tools/prize_gate.py key <candidate>` or `python3 tools/prize_gate.py scan <file>`. Only the uncompressed key of 1GSMG... matches its address
```
Useful OpenSSL flags:
-d decrypts data
-a tells OpenSSL that the encrypted data is in base64
-in <filename> specifies the file to decrypt
-out <filename> specifies the file to put the decrypted data in
```

# Walkthrough

## Phase 0 - The Bunny Image

[Link to notebook](./phase0.ipynb)

* "Follow the white rabbit"
* white/yellow square = 0, black/blue square = 1
* Unwrap the squares counter-clockwise
* 8 squares per byte, ascii
* result is "gsmg.io/theseedisplanted"

## Phase 1 - The Warning

[Link to notebook](./phase1.ipynb)

* Post a password on a hidden form to "https://gsmg.io/phase1verification"
* The URL and pictures form lyrics from the song "The Warning" by _Logic_
* The line following "Phase two" is "The flower blossoms through what seems to be a concrete surface"
* password is the line all lowercase, no spaces "theflowerblossomsthroughwhatseemstobeaconcretesurface"
* We are redirected to [http://gsmg.io/choiceisanillusioncreatedbetweenthosewithpowerandthosewithoutaveryspecialdessertiwroteitmyself](http://gsmg.io/choiceisanillusioncreatedbetweenthosewithpowerandthosewithoutaveryspecialdessertiwroteitmyself)

## Phase 2 - Mr Robot

[Link to notebook](./phase2.ipynb)

### Phase 2.1

* Using the url and the text we get matrix quotes, which leads to "causality" as the password for the AES, and is part 1.
* Decoded AES has Mr. Robot references 
* Parts 2,3,4 words can be found to be "Safenet", "Luna", "HSM"

### Phase 2.2

* Part 5 is "11110". It was first found by brute force, but the riddle can be read as a chain: a theorist with an equivalent current source is Norton (Norton's theorem), "insecure" is Norton antivirus, its "competition" is McAfee, the "belikins" are Belize's beer (where John McAfee lived), and "never execute an order that revokes the highest power or you might suddenly get killed" is John F. Kennedy's Executive Order 11110. "The 5binary code" is 11110 read as five binary digits. This is a reading, not something the creator confirmed. See also [EO11110](./unverified/11110.md)
* Part 6 is a reference to the Genesis Block of bitcoin, and directly to a particular line in the source code leading to "0x736B6E616220726F662074756F6C69616220646E6F63657320666F206B6E697262206E6F20726F6C6C65636E61684320393030322F6E614A2F33302073656D695420656854" as part 6
* Part 7 is a chess puzzle where a white piece must be moved without causing check-mate. The final solution is "B5KR/1r5B/2R5/2b1p1p1/2P1k1P1/1p2P2p/1P2P2P/3N1N2 b - - 0 1"
* Putting everything together with the case hints and white space hints we get the final password as "causalitySafenetLunaHSM111100x736B6E616220726F662074756F6C69616220646E6F63657320666F206B6E697262206E6F20726F6C6C65636E61684320393030322F6E614A2F33302073656D695420656854B5KR/1r5B/2R5/2b1p1p1/2P1k1P1/1p2P2p/1P2P2P/3N1N2 b - - 0 1"
* sha256 of that password is the key to decrypting phase 3


## Phase 3 - Free Will

[Link to notebook](./phase3.ipynb)

* First riddle refers to The Venus Project and the "thinker" is "Jacque Fresco"
* Second riddle refers to Alice in Wonderland, the answer to the quote is "just one second", password 2 is "giveitjustonesecond"
* Third riddle refers to the "Heisenberg Uncertainty Principle"
* Using the case and space hints we end up with "jacquefrescogiveitjustonesecondheisenbergsuncertaintyprinciple" as a final password

## Phase 3.2 

[Link to notebook](./phase3.2.ipynb)

* First blob is raw bytes that needs to be decoded with IBM EBCDIC 1141
* The resulting string is enciphered with a beaufort cipher (hinted at with "a beautiful strategic position")
* The key for the cipher is hinted at with "why am I here", a quote from the matrix, the next line being the key "thematrixhasyou".
* This reveals a long block of text: the Architect's speech from _The Matrix Reloaded_, with edits by the puzzle creator (it contains `TAKETHEPRIVATEKEY`)
* The numbers are enciphered with a VIC Cipher. The numbers are hinted at earlier with "one for one, four for one", use number 1 and 4.
* The alphabet is given below the numbers "fubcd oracle thingky mvps" which must be modified to remove the second "c" and replaced with either "." or "/", after which, the missing alphabet can be added to give "fubcdora/lethingkymvpszjqwx."
* Strictly this is a straddling checkerboard with blank columns 1 and 4 in the top row (key `FUBCDORA.LETHINGKYMVPS/JQZXW`). Of the 45 possible blank pairs only {1,4} reproduces the text. The 149 digits never use 7 of the 28 cells (`.`, `/`, J, Q, Z, X, W), so the order of the key's tail, and where `.` and `/` go, is a guess; the decode is the same either way. It decodes to:
  `INCASEYOUMANAGETOCRACKTHISTHEPRIVATEKEYSBELONGTOHALFANDBETTERHALFANDTHEYALSONEEDFUNDSTOLIVE`
* The last thing in the phase 3.2 plaintext is another `Salted__` envelope (the "Terminal", 80 bytes of ciphertext). It is still locked. See [the research status page](./unverified/gsmg-puzzle-kit-findings.md#4-the-three-locked-containers-v)

## Decentraland

[Link to notebook](./decentraland.ipynb)

The decentraland hint along with the [2020 hint](#2020-01-14-hint) were the path leading to [SalPhaseIon](#salphaseion)

To solve decentraland hint:
* Go to decentraland location given in image
* Click the box, a sound will play
* Download the sound
* Open in an audio manipulation program
* Split left and right tracks
* Inverse one of the tracks
* Mix both tracks back together to reveal the hint "HASHTHETEXT"

The scene's Decentraland deployment record covers parcels -41,-16 and -41,-17 and was deployed on 2020-02-20 at 15:12 UTC, 19 minutes before the creator posted the screenshot. Two days later the creator added "Only -41,-17 matters" (#1837).

Using everything we have so far, it points us back to the original image to hash the text on the image, which then
leads us to SalPhaseIon using:

```
SHA256(GSMGIO5BTCPUZZLECHALLENGE1GSMG1JC9wtdSwfwApgj2xcmJPAwx7prBe) = 89727c598b9cd1cf8873f27cb7057f050645ddb6a7a157a110239ac0152f6a32
->
https://gsmg.io/89727c598b9cd1cf8873f27cb7057f050645ddb6a7a157a110239ac0152f6a32

```



## SalPhaseIon

[Link to notebook](./salphaseion.ipynb)

* split the string into part based upon like encoded strings
* decode the abba string using a=0, b=1, convert binary to ascii string to give "matrixsumlist"
* Split the next few sections using "z" as a separator
* the "agda" and "cfob" string are encoded the same way
    * o=0,a=1,b=2..., hex string -> ascii
    1. agda = lastwordsbeforearchichoice
    2. cfob = thispassword
* the remaining abba string is "enter"
* the `agda`/`cfob` rule in full: letters a..i are digits 1..9 and o is 0, the whole digit string is read as one decimal integer, then written as bytes
* the plain-text pieces read `shabefourfirsthintisyourlastcommand` and `shabefanstoo`; with a1z26, `sha`+b(2)+ef(5,6) gives "sha256", so "sha256 our first hint is your last command" and (as a reading of `anstoo`) "sha256 the answer too"
* the two base64 pieces join into a third `Salted__` envelope (80 bytes of ciphertext), still locked
* the leading `dbbi...` block (91 letters) fits the poster's yellow/blue colour program at prime positions; the long `faed...` block (570 letters) has no known decode. A Bifid reading of `faed` (posted in the Telegram group on 2025-06-12) gives the header `btcseed` and nothing readable after it
* how `matrixsumlist` and `lastwordsbeforearchichoice` are applied to build "thispassword" is unsolved. See [the research status page](./unverified/gsmg-puzzle-kit-findings.md) for what has been tried

## Cosmic Duality

This stage is currently unsolved. It is the second textarea on the SalPhaseIon page, a `Salted__` envelope of 1,328 bytes of ciphertext ([base64](./unverified/gsmg-puzzle-kit/cosmic-duality.b64)). No password that gives readable output is known.

A "checkpoint" shared in the Telegram group since August 2025 claims Cosmic Duality is "correctly decrypted" to a binary with SHA-256 `4f7a1e4e...c081` (the key is the XOR of the SHA-256 of several SalPhaseIon words, used with the old MD5 key derivation). That output is noise: it ends in a single `0x01` padding byte, which about 1 wrong key in 256 also gives, has 7.87 bits of entropy per byte, and does not compress. The same goes for similar "unlocks" of the two short envelopes. See [the research status page](./unverified/gsmg-puzzle-kit-findings.md#padding-only-unlocks).

# On-chain messages from the puzzle

The P2SH address `3GSMG24TujqfMJG1kQoBX18DzJHQLeJYMK` sent small payments with `OP_RETURN` messages to addresses whose private key is the SHA-256 of a known answer (compressed public key). Every address below was re-derived from its answer and every message read from the chain on 1 Nov 2026.

| date | block | sent to | private key is sha256 of | message |
| --- | --- | --- | --- | --- |
| 2020-03-24 | 622762 | `1GyT5WrLYpwFkuiVoPDJZa1Q6jtjbjuBff` | the prize address `1GSMG1JC9wtdSwfwApgj2xcmJPAwx7prBe` | `GSMG.io: do you beleive me you need it?` |
| 2020-03-24 | 622762 | `1Jqq37KkZEt4F3Dt6qXdtyiMEFBBdawbkJ` | `causality` (phase 2.1) | `GSMG.io: Right, this is causality` |
| 2020-03-24 | 622766 | `18CchrjA3Uzfrzy4DFqao9ric6YfK4hjdc` | the 149 checkerboard digits (phase 3.2) | `GSMG.io: part of the cipher` |
| 2020-03-24 | 622767 | `1AD2wfwXukZ1kUAy848hTQQ72aSBZPB75r` | the phase 1 password | `GSMG.io: are you sure?` |
| 2020-03-24 | 622767 | `1K23RS1y2fnuZRkhw5nUpFr5Jk5WN11Zeq` | the phase 3 password `jacquefresco...` (62 characters) | `GSMG.io: phase3.2 pass OK` |
| 2020-03-24 | 622774 | `1M5ypvDbp124ZtKPbg3GJg1JqNs1x7TPoN` | the phase 2 password (227 characters) | `GSMG.io: You are here because 227 chars were correct` |
| 2020-04-03 | 624209 | `148XH2YBmLr4oAJXQcG84FpNYoBmqnVPHQ` | (not hashed) `gsmg.io/theseedisplanted` as a big-endian integer | `Good job, Neo!` |
| 2020-04-03 | 624209 | `13HGhjkmKUkP8sk9k63BLmhkxRjy7uK4Rp` | (not hashed) the same 192 bits in reverse order | `Good job, Neo!` |
| 2020-05-11 | 630001 | `1GSMG1JC9wtdSwfwApgj2xcmJPAwx7prBe` | | `Halving` |
| 2021-07-18 | 691563 | four addresses | the prize public key P moved by one curve step: P+G, P-G, 2P and P/2 (uncompressed) | `GSMG.io neighbors, half and double` |

Why this address is the puzzle's own: the 2020 halving transaction, signed with the prize key, spends the 700 sat output of the `Halving` message transaction, and the two sit next to each other in block 630,001. The 2021 "neighbors" payment also shows that the uncompressed public key is the one in use.

These messages only confirm answers that are already known, so they do not lead anywhere new. Since 2025 other people have sent `OP_RETURN` messages to and from these addresses ("From Neo", "BULLSHIT", "Neo wallet ...", and others). The private keys of the checkpoint addresses are public, so anyone can, and those are not creator messages.

# Further Hints and 2020-present Timeline

At the end of 2019, and early 2020, no one had publicly made progress passed the AES blob in phase 3.2. The following are either official hints, or various quotes that _might_ be hints.

Notes on the sources:
- Quotes are from the creator's Telegram account, "Jrk Bgrt" (handle `@SoWut`), in the GSMG Puzzle Solvers group. Numbers like `#8000` are Telegram message ids, so a quote can be found in any export of the group.
- The dates in the headings are as the screenshots or exports show them, in local time (the Telegram exports used here are in US Eastern time). Posts late in the evening can fall on the next day in UTC. Times given as UTC below were taken from the export's Unix timestamps.
- Many of the creator's old posts were edited in 2025 and 2026 (for example #6884, #8000, #8330 and #66574). The wording now shown may be newer than the post date. The screenshots in [hints/](./hints/) were taken before most of those edits.
- An account named "Double shot of Jameson for Jrk" posted in January and February 2026. It is not the creator.

## 2019

- 2019-04-20 (#74, #75): "Ok.. somebody has cracked the first code." "that was way faster than expected."
- 2019-04-22 (#225): the creator posted `5ac407837447fba24ba2802e4d1e9aecb4580aa29fef1088cc387c180b746f75`, the SHA-256 of the phase 1 password, so that solvers could test guesses offline instead of on the overloaded site.
- 2019-05-08 (#660): "somebody managed to get into Phase 3".
- 2019-09-26 (#1487): "There may indeed a piece be found outside the main puzzle."

## 2020-01-14 Hint

The creator gave a hint on the Telegram group on 2020-01-14:

![Roses are red](hints/2020-01-14-roses-are-red.png)

```
Roses are White but often Red.
Yellow has a number and so does Blue.
Go back to the first puzzle piece without further ado.

It might have shown you only one door, beware that the rabbits nest may contain a whole lot more.

Hush hush.
```

Unfortunately, no one publicly managed to decode it

## 2020-02-20 Hint

The creator gave a second hint: a screenshot from within [decentraland](https://decentraland.org/) at -41,-17 

![Decentraland hint](hints/decentraland-tg.png)

See how it's solved [here](./decentraland.ipynb)

On 2020-02-22 (#1837): "Only -41,-17 matters".

## 2020-03-24

The six `GSMG.io:` checkpoint messages were sent on chain, confirming the answers to phases 1 to 3.2 (see [On-chain messages](#on-chain-messages-from-the-puzzle)). The same day, asked whether the private key is in the last cipher of phase 3.2, the creator answered (#2918): "There must at least be something hidden in there."

## 2020-04-08

Posted from the creator's own account (#3390). It is word for word a line of the Architect in _The Matrix Reloaded_. It came one minute after a solver asked "The door that leads to the source?", but not as a reply to it.

![Humph. Hope, it is the quintessential human delusion, simultaneously the source of your greatest strength, and your greatest weakness.](hints/2020-04-08.png)

> Humph. Hope, it is the quintessential human delusion, simultaneously the source of your greatest strength, and your greatest weakness.

Earlier the same day (#3338): "Those hints are the last hints. Although I can say that one team managed to find something... something others haven't yet found (unless they didn't tell us)."

## 2020-05-11

Bitcoin halving. Half of the prize was moved to [17ucy1K9ZUAaoY6JVtM932W9jUp5LXfyHa](https://www.blockchain.com/explorer/addresses/BTC/17ucy1K9ZUAaoY6JVtM932W9jUp5LXfyHa), in block 630,001 (the halving block was 630,000). The same block holds the `Halving` message from the puzzle's own address (see [On-chain messages](#on-chain-messages-from-the-puzzle)).

And Jrk mentions a second door.

![Alt text](hints/2020-05-11.png)

## 2020-06-07

The first public mention of SalPhaseIon (in the `#Crypto_Puzzles` discord channel)

![Alt text](hints/2020-06-07-salph-discord.png)

## 2020-08-02

Another mention of the extra door

![Alt text](hints/2020-08-02.png)

A week later (2020-08-09, #4624), asked whether solvers are looking for a private key, a seed phrase or a brain wallet phrase, the creator answered: "a private key".

## 2021-01-21

Jrk hinting that people have reached the final stage. It can be seen from the Telegram chat, and discord chat - in retrospect - that some groups may have reached the final stage in late 2020, but did not publicly declare it. This is the first time it was confirmed someone had reached it.

![Alt text](hints/2021-01-21.png)

## 2021-02-12

The first mention of SalPhaseIon in Telegram

![Alt text](hints/2021-02-12-salph-mention.png)



## 2021-03-01

We get confirmation that spelling errors are not significant.

![Alt text](hints/2021-03-01-spelling-hint.png)

And we find out that there is a "prime part"

![Alt text](hints/2021-03-01-primes.png)

## 2021-03-14

"Fyi. Another person (or team) made it to salph." (#6491). Then, answering how the creator knows this (#6497):

![Alt text](hints/2021-03-14.png)

This was long read as confirmation that SalPhaseIon is the last phase, but the message does not say that. In 2025 the creator called yinyang "the next phase" (see [2025-04-28](#2025-04-28)). Later that day, asked for a hint on `matrixsumlist` (#6509): "I gave an unforseen hint already". On 2021-03-22 (#6712): "Nr 5 in salph".

## 2021-04-01

The creator posted (#6884): `Hint: "another door might be found on {1 },{4} ,{21}"`. Asked on 2021-04-18 whether it was a real hint, the answer was "Do you know what usually happens on the first of april?" (#7529). Later on 2021-04-01:

![Alt text](<hints/2021-04-01-april fool.png>)

Two later observations use these numbers, both unconfirmed: the phase 3.2 checkerboard has its blank columns at 1 and 4, and subtracting the checkerboard message from the `dbbi` block letter by letter gives a string with `V`, `I`, `C` at positions 1, 4 and 21 (see [the research status page](./unverified/gsmg-puzzle-kit-findings.md#readings-that-are-not-tested-or-not-confirmed)).

## 2021-04-16

The contents of SalphaseIon leak to telegram

![Alt text](hints/2021-04-16-salph.png)

The same day a solver wrote "Go to the first puzzle piece (image) and hash all the text you see. But mind that the author is a bit picky what he considers to be text." (#7416), and the creator replied "Good point" (#7418).

## 2021-05-06

The exact text to hash is posted (#7616, 2021-05-07 00:47 UTC). It came from a solver's account, since deleted, not from the creator.

![Alt text](<hints/2021-05-06-salph instructions.png>)

### Discussion
It is revealed that the way to get to salphaseion is by taking all the text on the initial image - including the bitcoin address - and then taking a hash of hte result will give you the url needed to enter salphaseion.
```python
>>> import hashlib
>>> h = hashlib.sha256()
>>> h.update('GSMGIO5BTCPUZZLECHALLENGE1GSMG1JC9wtdSwfwApgj2xcmJPAwx7prBe'.encode())
>>> h.hexdigest()
'89727c598b9cd1cf8873f27cb7057f050645ddb6a7a157a110239ac0152f6a32'
```

And so [https://gsmg.io/89727c598b9cd1cf8873f27cb7057f050645ddb6a7a157a110239ac0152f6a32](https://gsmg.io/89727c598b9cd1cf8873f27cb7057f050645ddb6a7a157a110239ac0152f6a32) is the link to SalPhaseIon

See how to [solve it here](./salphaseion.ipynb)

## 2021-07-18

The puzzle's address sent 5,000 sat to each of four addresses with the message `GSMG.io neighbors, half and double`. They are the addresses of the prize public key moved by one curve step (P+G, P-G, 2P, P/2), uncompressed. See [On-chain messages](#on-chain-messages-from-the-puzzle).

## 2021-08-11

Asked "Do you mean the encrypted private key stored online?", the creator answered "The one to be found by solving the puzzle yes" (#7832), then "And the solver will find a way to 'decrypt' it." (#7834).

## 2021-12-02 Hint

Another Official hint

![Alt text](hints/2021-12-02-another-door-hint.png)

## 2021-12-26 Christmas Hint

Another Official Hint

![Alt text](hints/2021-12-25-hint.png)

## 2021-12-31

Asked personal questions and the private key in one message, the creator answered (#8048): "The only date I give away is the expiry date of neo's passport." In _The Matrix_, Neo's passport expires on 11 September 2001.

## 2022-12-10

Picture of a book called Cosmic Duality

![Alt text](hints/2022-12-10-cosmic.png)

Book cover:

![Alt text](hints/cosmic-duality-book.png)

The picture was posted by the solver barrystyle (#8310). The creator replied "That is very specific" and "If the puzzle is solved you'll see how scary specific that is" (#8311, #8315), and on 2023-01-09 "@barrystyle, provided a very specific hint already." (#8328).

## 2023-01-09

Confirmation that prime number is important 

![Alt text](hints/2023-01-09-prime-number.png)

## 2023-01-12 - Hint

The theory of everything is a hint

![Alt text](<hints/2023-01-12-theory of everything.png>)

Two minutes earlier (#8352): "I checked a certain GitHub yesterday, for whoever set that up, nicely done. You guys are really getting close."


## 2023-02-23 - Official Hint

A seemingly binary string was posted as a hint, It's decoded to 
```
yellow blue primes matrix sumlist last words before archichoice yinyang 
we wont give away thepassword its in front of  your eyes but youre 
not seeing it very last step is a true give away promised
```

![Alt text](hints/2023-02-23.png)

## 2023-06-10

A solver wrote that phase 3.2 "is not totally solved, as the final block hasn't been decrypted" (quoting the Terminal envelope), asked whether the SalPhaseIon hint was there, and asked about the phase 2 line `X 2 S H 4 Y 0 Q B 15`. The creator answered the three in order (#8569):

> Correct.
> \-
> No.
> \-
> Can't say anything about this.


## 2023-08-03 Hint

"Are you really looking for just the btc...?"

![Alt text](hints/2023-08-03-1.png)

"the hardest part is done."

![Alt text](hints/2023-08-03-2.png)

### Discussion
It can be noted that the "..." we see in puzzles shows up, and might be replaced with "key". The whole sentence can be reinterpreted as meaning "Look for the key"


## 2023-08-06 Hint

![Alt text](hints/2023-08-06-1.png)

![Alt text](hints/2023-08-06-2.png)

![Alt text](hints/2023-08-06-3.png)

![Alt text](hints/2023-08-06-4.png)

Also that day, asked whether there is another URL to find or whether to brute force (#9607): "No need. You have all the info." And later (#9627): "Something was solved rather... remarkable."; asked when (#9636): "I have no clue."

## 2023-11-24 to 2024-01-26

- 2023-11-24 (#16624): 'There's a question multiple people have asked me. "Given the available knowledge, is internet still required to solve it?" Nope'
- 2024-01-26 (#20223), asked what format of key is being looked for: "Regular Bitcoin Private key". Asked in the next message for a hint on "our first hint is your last command", the creator replied only with a zipped-mouth emoji (#20224).

## 2024-04-10

"1357 blocks to go" (#24071): a countdown to the halving at block 840,000.

![alt text](hints/2024-04-10.png)

## 2024-04-19 Second halving

![alt text](hints/2024-04-19-1.png)

![alt text](hints/2024-04-19-2.png)

## 2024-11-29

- "If wallet != empty, puzzle not solved. (Most likely)." (#32535)
- "If you guys got 1 microstep further, the puzzle will likely be solved the same day. ... And in the end, good puzzles don't need hints" (#32579)
- "I think I'll be going for ASCII 127 myself. But not overly dramatic." (#32613), in a joking exchange about which character to imagine oneself as. ASCII 127 is DEL.
- A post forwarded on 2024-12-02 (#33445): "You're going too fast now. Same software was used in every phase."

## 2025-04-28

- "If I'd ever take the funds (I won't), I wouldn't even tell the answer" (#39219)
- "Did anyone found yingyang? I don't think so, you guys are so smart, when yingyang is reached, 2 hours max." (#39224)
- Asked "is yinyang found after decoding an AES ciphertext?" (#39233): "It's the next phase, but I await the day someone finally gets there." (#39237)

"yinyang" is one of the words of the [2023-02-23 hint](#2023-02-23---official-hint).

## 2025-10-17

A creator post, forwarded into the group on 2025-10-17 (#50656) and again on 2026-09-12 (#71627), reads `53 75 72 65 62 75 74 77 65 77 6f 6e 74 67 69 76 65 69 74 61 77 61 79`. As ASCII hex this is `Surebutwewontgiveitaway`. The original post is not in the export.

## 2026-01-01 New Year's Hint

![new years hint](hints/2026-01-01-new-year-hint.png)

### Decode

Use a simple ["binary to ascii" conversion](https://gchq.github.io/CyberChef/#recipe=From_Binary('Space',8)&input=MDEwMDEwMDAgMDExMDAwMDEgMDExMTAwMDAgMDExMTAwMDAgMDExMTEwMDEgMDAxMDAwMDAgMDExMDExMTAgMDExMDAxMDEgMDExMTAxMTEgMDAxMDAwMDAgMDExMTEwMDEgMDExMDAxMDEgMDExMDAwMDEgMDExMTAwMTAgMDAxMDAwMDEgMDAxMDAwMDAgMDEwMDExMDEgMDExMDAwMDEgMDExMDEwMTEgMDExMDAxMDEgMDAxMDAwMDAgMDExMTAxMDAgMDExMDEwMDAgMDExMDAxMDEgMDAxMDAwMDAgMDExMDAwMTAgMDExMDAxMDEgMDExMTAwMTEgMDExMTAxMDAgMDAxMDAwMDAgMDExMDExMTEgMDExMDAxMTAgMDAxMDAwMDAgMDExMDAxMDEgMDExMTAxMTAgMDExMDAxMDEgMDExMTAwMTAgMDExMTEwMDEgMDExMTAxMDAgMDExMDEwMDAgMDExMDEwMDEgMDExMDExMTAgMDExMDAxMTEgMDAxMDExMTAgMDAxMDAwMDAgMDEwMDExMTEgMDExMDEwMDAgMDAxMDExMDAgMDAxMDAwMDAgMDExMDAwMDEgMDExMDExMTAgMDExMDAxMDAgMDAxMDAwMDAgMDExMDEwMDAgMDExMDAxMDEgMDExMTAwMTAgMDExMDAxMDEgMDAxMDAxMTEgMDExMTAwMTEgMDAxMDAwMDAgMDExMDAwMDEgMDAxMDAwMDAgMDAxMDAwMTAgMDExMTAxMDAgMDExMDEwMDEgMDExMDExMTAgMDExMTEwMDEgMDAxMDAwMDAgMDExMDEwMDAgMDExMDEwMDEgMDExMDExMTAgMDExMTAxMDAgMDAxMDAwMTAgMDAxMDAwMDAgMDAxMTExMDAgMDAxMTAwMTEgMDAxMDExMTA)


Copyable:
> 01001000 01100001 01110000 01110000 01111001 00100000 01101110 01100101 01110111 00100000 01111001 01100101 01100001 01110010 00100001 00100000 01001101 01100001 01101011 01100101 00100000 01110100 01101000 01100101 00100000 01100010 01100101 01110011 01110100 00100000 01101111 01100110 00100000 01100101 01110110 01100101 01110010 01111001 01110100 01101000 01101001 01101110 01100111 00101110 00100000 01001111 01101000 00101100 00100000 01100001 01101110 01100100 00100000 01101000 01100101 01110010 01100101 00100111 01110011 00100000 01100001 00100000 00100010 01110100 01101001 01101110 01111001 00100000 01101000 01101001 01101110 01110100 00100010 00100000 00111100 00110011 00101110

Decoded: 
> Happy new year! Make the best of everything. Oh, and here's a "tiny hint" <3.

### Observations

- Each message is purposely 1 minute apart
- Again, we're given binary text
- There's mention of a hint, but what the hint is referring to is ambiguous.

## 2026-03-04

(UTC; the evening of 2026-03-03 in US time)
- "No hints , only free will." (#60289) and "Jacque was quite an inspiring lad I'd say." (#60298)
- Asked "Are we really looking for just the btc...?" (the wording of the 2023-08-03 hint): a zipped-mouth emoji (#60307).
- A solver claimed to have extracted "ying yang" and "salvation" with prime indexes on the last words. The creator answered (#60314): "I only need to look at the address. If any of you reaches the next phase, the price is taken in no-time."

## 2026-04 to 2026-08

- 2026-04-13: a forward of the GSMG company's farewell post, "The End of GSMG" (#61385). The gsmg.io sites went down over the following weeks (alpha.gsmg.io by 2026-05-22).
- 2026-05-28, asked whether the sites being down affects the puzzle (#63957): "Ah, ofcourse. The puzzle is still valid!"
- 2026-08-18: solvers reported "Original site up now, gsmg.io" (#69025), with `gsmg.io/robots.txt` now showing a rabbit. Pages served by the relaunched site may differ from the archived originals; compare against [archive/](./archive/) before relying on new details.


## 2026-07-12 hint

![July 2026 Hint](hints/2026-07-12-official-hint.png)

(#66573 and #66574, 2026-07-13 00:51 UTC. #66574 was edited on 2026-08-23.)

> Jrk Bgrt
>
> My close friends have the best chance of solving it (a few tried). But they don't have the skills some of you do.
>
> NOTE: that is a hint.


## 2026-07-12 Other message

![July 2026 other message](hints/2026-07-12-other-msg.png)

> Oh... and before I fall asleep. I want to assume it is quite clear I held quite a secret in my head which I seriously wanted to share with the planet... for those who can understand what I meant... (#66592)
>
> The "5" btc was never the actual prize. That was only a tiny fraction. (#66593)

Other lines from the same evening (2026-07-13 UTC):
- "Most of you know the puzzle WAAAY better than me at this point. I have a hidden laptop which I haven't touched in years. On that thing... is the actual answer...." (#66568)
- "I feel it a bit off knowing the url (and thus the original puzzle) is "gone"." (#66584)
- Asked "salphaseion is 100% solveable?" (#66587), three minutes later: "Yes" (#66588, not threaded as a reply). Then: "And IIFF I'm somehow still wrong, which I'm most likely not as I've verified many times back then after some sad rushed mistakes, it's all still solvable with a few stable qubits." (#66589)
- "(And yes, the btc is still available before you fire any questions)." (#66595)
- "Some already found it. And understood not to risk it..." (#66600)

## 2026-07-16

- About the laptop: "Well, it's hidden in a room with a hidden door." (#66903)
- Replying to "I don't think fractions can be prime.": "You have to be in your prime for that." (#66931)
- "Give yourself yourself and yourself will be given yourself." (#66961)
- Replying to someone waiting for the next "NOTE: that is a hint." moment: "Latetly, I'm working with many NOTES." (#66962)

## 2026-09-01

The last posts by the creator in the group as of the 8 Oct 2026 export. After this date there are only forwards of older posts.

- "Pfff. Coincidence." (#70307). This came about five hours after a solver's post (#70303) that `YOUWON` appears in the `dbbi` minus checkerboard string, that positions {1,4,21} spell `VIC`, and that `enter` maps to Executive Order 13224. It is not threaded as a reply, so what it refers to is an inference.
- Thanked for the puzzle and asked how it could be afforded: "A. I rushed (t)it. B. Yes, have quite some time for stupid stuff." (#70311)
- Asked whether `dbbi` and `faed` are meant to be decoded like the other SalPhaseIon segments, or are only an ingredient: a zipped-mouth emoji (#70325).
- Asked how long the puzzle took to make and whether it was a solo effort: "Couple hours, and no." (#70336)
- Asked whether it was not "two sloppy days throwing one together": "Same same" (#70377)

