# diy-synth

Schematics and related files for DIY modular synthesizer components.


## MS-20 VCF

![MS-20 PCB, 3D view](./pictures/VCF_MS-20_front_3d.png)

A voltage controlled filter based on the "late" Korg MS-20 design. Original design schematics from [Rene Schmitz](https://www.schmitzbits.de/ms20.html) and [Eddy Bergman](https://www.eddybergman.com/2019/12/synthesizer-build-part-12-korg-ms20.html?m=1).

**Working Falstad circuit simulation (online):** [click here][1]

### Features

* Designed for Eurorack format with a 6 HP frontplate and standard +/- 12 V power supply.
* Frontplate potentiometers to control filter cutoff, resonance, input level, and cutoff CV amount.
* Input jacks for source audio signal and cutoff CV; output jack for filtered audio signal.
* Quad opamp (LM324N) and dual OTA (LM13700) in the main circuit.
* LEDs in the resonance feedback circuit indicate resonance "drive".

### Layout

* Circuit schematics: [VCF_MS-20_plan.pdf](./schematics/VCF_MS-20_plan.pdf)
* Board layout: [VCF_MS-20_pcb.pdf](./schematics/VCF_MS-20_pcb.pdf) ([*mirrored*](./schematics/VCF_MS-20_pcb_mir.pdf))
   * The board is a 21 x 36 hole (56 x 97 mm) perforated PCB that should fit in most Eurorack cases. The required depth is about 60 mm.
* Board layout with frontplate design: [VCF_MS-20_pcb_all.pdf](./schematics/VCF_MS-20_pcb_all.pdf)
   * The frontplate is designed for Eurorack cases and has a size of 3 U x 6 HP (127 x 30.5 mm)


### Components (BOM)

*Estimated costs ~ 25 Euro* (in Germany, as of Nov 2023)

|Item |Qty  |Reference(s)                  |Value          |Datasheet                                         |Note           |
|----:|----:|-----------------------------:|--------------:|--------------------------------------------------|---------------|
|    1|    1|                            C1|           4.7n|~                                                 |               |
|    2|    2|                        C2, C3|           1.0n|~                                                 |film cap.      |
|    3|    2|                        C4, C5|           100n|~                                                 |               |
|    4|    1|                            C6|           1.0u|~                                                 |optional       |
|    5|    1|                            C8|           470n|~                                                 |film cap.      |
|    6|    2|                        D1, D2|            LED|~                                                 |               |
|    7|    1|                            J1|          POWER|~                                                 |               |
|    8|    1|                            J2|       AUDIO IN|~                                                 |               |
|    9|    1|                            J3|      AUDIO OUT|~                                                 |               |
|   10|    1|                            J4|          CV IN|~                                                 |               |
|   11|    2|                        Q1, Q2|         BC558C|https://www.onsemi.com/pub/Collateral/BC556BTA-D.pdf|matched      |
|   12|    1|                            R1|           200k|~                                                 |optional       |
|   13|    2|                        R2, R3|           100k|~                                                 |               |
|   14|    6|       R4, R5, R6, R7, R9, R10|            10k|~                                                 |               |
|   15|    1|                            R8|           8.2k|~                                                 |or trimpot     |
|   16|    1|                           R11|           4.7k|~                                                 |               |
|   17|    1|                           R12|           470k|~                                                 |               |
|   18|    1|                           R13|           2.2k|~                                                 |               |
|   19|    1|                           R14|           1.5k|~                                                 |               |
|   20|    4|            R15, R16, R17, R18|            220|~                                                 |               |
|   21|    2|                      RV1, RV4|    100k / log.|~                                                 |Resonance ctrl.|
|   22|    2|                      RV2, RV3|    100k / lin.|~                                                 |Cutoff/Input/CV ctrl.|
|   23|    1|                           SW1|     SW_DPDT_x2|~                                                 |HP/LP mode     |
|   24|    1|                           SW2|       SW_SPDTT|~                                                 |6/12 dB falloff|
|   25|    1|                            U1|          LM324|http://www.ti.com/lit/ds/symlink/lm2902-n.pdf     |               |
|   26|    1|                            U2|        LM13700|http://www.ti.com/lit/ds/symlink/lm13700.pdf      |               |

Notes:
* Use film capacitors in the audio signal path, not ceramic ones. (Ceramic ones have a voltage dependency that causes distortions.)
* The feedback resistor R8 may be tuned to change the resonance characteristics, e.g. a trimpot could be used instead of a fixed resistor. Check out the [circuit simulation][1] to see what this does.
* For best results, the two transistors should be matched by their hFE value as good as possible. This can usually be done with a simple multimeter with transistor tester.
* A passive low-pass filter (R1/C6) is added at the audio input to remove any DC voltage offset. This is completely optional and the components could be removed from the circuit.


[1]: https://falstad.com/circuit/circuitjs.html?ctz=CQAgbArCAMB00OgRgCwE4Oa9kAme0AHBBAMxhq6lKEDsYt4uISzGMBiSAUCtMyiRg8fEBFYjoLGAB0AztHl95AWlbzFCjbCibNyueq3G4u+UlVI49amFK1SpCLRpG4KUkRpokaMNAg0IipzBHkAEwBTADMAQwBXABsAF1lDVXdPQm9ff0Dg0m0PALAUXH8qXGgnFFDNKLik1M0LE1hiiFLy-lIqmrqImISUtNa1JHg0QQh0NFJCXFxOiCLcFzpqANol3pQVwzC5BuHm80sJ3BRaaG3CDbBSpEKFWHswXFY7h4+iHwGjoZNNJqVbrbp0Si+ba0DLtcqUbIOPi4KZ-A71QEjTQg4wqdzw3CI0jI1GtKwYxpYyzyRawFFIWh0D7XB7IMCwspg-wQj5oaH-Y5A7GtOBvH4oQh8hYQQgoSCw+yBToLQlVJDOZ7kwaU05yHHY0W0JVgFULZAagWY3U4wiwWUea78YhlB5jQ3vKwSqVLWXy9Hak6jDSrChUa60dA3NAQXCWnVBvX4lyMlG7QjQFCCEOUew3SO0aOx-0A+MtSykHTocjQSDZdVGwighkLOaXdOZsmHQVU9K4uDVMoS3zUQQ3ba1Yvd3Ui7Rs7bvLJWchgdVxk7cWLgFCSFgSS5SQgsZhqZjkxBSftOWwFwJOD6eZiXsgM1A+aoMqiHs8IDcgOXb8YBCEEBAJANAjxAiRvwQED+3PGVxGoZkyiQGgZl0Fhz2gbgAHcjy-Sg-wIx9cPwndUOYfcYFIiUWEI2jFm3bC8IYy4tzwNjmLEQjGLEegOKY0jnGEXjhLoki8LE3xmEgYRpOovDZJ3UopCorjxEo0QxLUoT+Ko7TOgUviRMMwJKMMriGNEBiLJow8lmEUo8FsvDeikQRhFojyjJszzD08QTJL00z+IC6iAGMiJAMLaMcYQpCQSIVHAlR8BNXlCDvGsqEIuCeEisSwsK8gYBYJLwPwPhiXeWtnUCBwOAQHgWP8kqvOA7CACcWEzcieNEBLzxomCqkPbzRqM+ZtyEdzgJmoylPkxb-AWwz5v-FgVq6v85pWjb5sGxBuG60D5pUJyDswo68NOla1F6g7SPO6aVs+TaL1It6GTkwlxOo7qprwO5otlaKStUqpjrBkTgbi6HSsWLjAcJfzQbWCT4fRzHge2+7txRyDerhiHcfkgm1EI4mONxhyd1Sogd0On8TvIfyYxA1m-xg1SsO4SKVD4KQwoF3poozUq4K4DhMwwbKHnEdsXEa5Ans5u8OZNMXBO67yPAEJy9YRqpLJgw3ddF7ChGYOGNK5qRbeYKcVESSJwmkC9Gp4K27bEImSpmfGQCdl23aQCXPdIm2JDcsQJCR-2iaqX3AuipOA9T+24+G9zRcBw2Tft3rBdjkiAba9MQe3CUPbNJHQern2G-jvyhaTpvuAZbc7hz5hu+izWw+gjgFgYLCx7DgAlSI5AAewAO1iOfwsiJ7DeFhuwuw1JUAAivvpAiupDUWD4HEOYHHQp4Fkyw88R0BAKDIfgM3QI0w4gGCp24VJyYr2mVEPpBXcsBWCoGyBQBwDYygn0zHQGM0A-AfElNsKAH8pBfxuqLQBh8aJ+DwAzdAwgcEsTwRXDaOCdbATIU5QB34oYHncoeWhQ08L-ycv-Dqn1+LJTktwiiRl96gQ4VnVhhkhFiLwVxYR1sSqgW2nDUCgM5F-kdHzH2PD1FOXcrAR0Y8sKJWShwBCTwWQbEcPVZWzV1F4OLnI7OIEDYwQFoeAuIFaKCNolxDxX5uFaJok5DRDcNGWQroE0Jni7JHy8k4iJ3VBGi33h1FRLCWDcPcdwi2n1eoAIShIHJRk1AiWsvZAapElJUWuPjUpN1i7CzVuLEJIA-6GWITtIhqkWkfWRJBPcohCnkTSPoYURY9DaDMMYAwbhgwvHGWMKwOi3iEEgFMRkxByhFEXJKKEVwaylE1F2K0CY77FGyFsvkOyHgeA2SUMogQMBUBUvsikgYyxtA6F0O5OZHlriFGcPUqEQF+FYMUQkQgVwwheHwIQko1jvD4IQiFWoSwvL+eMEBJIyAFlbOmZ4+J+AYGfGfdU6zJyHOFEUNkayoyMmjMgZ4xzkAeFQFNJwfI-A-J7PqDkjKRwsvquy0lpZqRyFpKQc+DgUTlCeP+bl0L4EFhpR-J4HLrQijhPi9AgsEFzFQByY2VUIzIHNHYRFByhX-Omcc-V1RDVWHVCalVwIyQTGBcSI0rN6ARj1RqqYiAMAjkda8vQ7RGVrDuPaGsGZ2SCpRb2Bl0LmQ7HJCMkNqAw13EzJGuUgbUUAsqFUa4dwnj2v2O4SlibnwICLEiqcCZg0IHTMgFE58+AXz9DWslfyDTwCsNyaM+Q9gLEcBODtOpVaUQZioLBH1XKg1ArY-hllgLzqcYu-xAE3pBLettfhU7TxQXiiwNBn08kJLyRQtxt9AH5KZj+TukFfqgRPLfdxV1EAcF6DQPRWFSAgAAMLxGSDPaI0Qnq7vCVemdpV8ngY+gAcw1mNJxnNvLwcgpTWR8l1ZobxvDXD2HqIIbhsRkqBHsJEdBsRyj7M0MxlasIW2VNyN-gNqLBu+dCNESPpuvBz6JbcAQ-wua0dHzUQng+l9t83r9I9qIOOEsdDcHE3xp90md7hz6fJi8inlN0bw50IW4M-xi0GuHUwHdrggQdtsKzK0sZh0RtFeBmEWDcAAMqXqFuLFQjGGmlTiIkOQkQEZPWs8eB2ONQu-QUYx8GoXo6yMY0nbCnNnFeYAhvAepUACSc9uCczelRQrNmw4JTkMkeQAB5QD+XNblNEOUkrCM57hCqzVgr57cnHi+qVAAQgAS1iHIfLlmOEmWEAk-jm487ATht5cCeSoJjxYHSK4TxOh8hNAWdUK3LguHeEyWUkqGBvp-K5Nus22qcIQ33Q2t3PFidSXJXhfkNPcdE9piAAmgaQa1gfD22FKtNL-gzPwPMvwCN+kV3qOkbr8ImhTCdLiwP9W4zxSLcOYfA1w1jLiOObNCJs3j9TWMcfVPQ5pI+E1YeEyqdxh6W1Pq-XkoV8nxcJpwwmlIwyVFOfk754ZkSRPI4lV56Lhmdd8Y2fGsLxSPOGtrVypHUG81kay+chN8y7TqKbjMspUQVEvzddPMtyqA55hwrlJlGMUAzfVXKDKOqfJf3QVVprOp4tN61bGmNYCXlX1SAAGKRFdgAI1iOFAA1rwaopUG78PTglDwAB9QgyfoDJ48DMZPVgc-4DT2oZPuAc8p9IDH39Md+lr1E6hWgqf0+Z6vDnjPksEH0E6EsZPhfi+1+T2Xj4Yc+5UU24zaQM0YJWKHwzIf5OZ8HgrpzLiSyq4wT18XFLms1+r-ogHkAU9Z4LyXivSS9EYJ525uXsQv0G4qWTqVdUGe08Z6zygZPEB08gK70gIvOeP59+97Tu9IAT1mVhVnILlgAYDKrirszs1q1uAXlnhJlEjsDuDj5KbGxqbK0sXOxqviIhnFxgQahpHG3AvmnFnFVEwNuGFA4BNprLku-k-o3tnrnqwHaF-j-qhO-mXpQalMDLxokltEeqQPXs-jUB-vap3nAAXt-j3mQP-rwXpt5ALFgR7KhCIUwS-s3hIRwT3k8AobHngmFLxIvruK-poeIbnnAN-t3jnqgAYb+rxEYezJdOqOYQ3lodYR3u-tYbob-q-jwbHpKD9F+PwNNLlEeBoR4ZYS3p-oXvlCAIyPjNPqLFzn+Dot+mPBAElIwNIVMJlFbs7iavYJYqRLQfgoeEkRUUZJUk9okeLPJFxLURUuLLxE0Q0XpMDPvF4szvxF9IzgAB6JE7ZoSJEPTAzTTbjRrhC9akQEyJK9HxRzHy4JSo7UQeblETTNES7+axCBbBaqTcBDEuD4zzCJHiAiBhyTFHgRCzGSTRaaypQ2aL7uZiArTqx6YEZhwBZBYhZBQTb+yhQ0a6QTbswGZOYkQeZTqe7eZYyby7H7F-EgRwlJxPHWz0FPRYzkxYnk5ol0y0w6RDHQkV4lF8FQDEjuQ9QgAAASAACkcRzCNJlMicyYSJ5FSQADL0lDFkAAn2xkBgy-rXFckMkzBCzZBiAyiVzGaoA0n0lw48STpkylKUH7zglhTchx6MHRHyH4A+EECSHv62F7AOF1GEJ-aJ5-juFiG6k6Af4IBIRGmyGZ4BGX77xrzixNyxyiHMEiF6n2lNTRiOl+HiD-4zy7gu6Horh7DTTaZSyqQRnRTcDhnqFNKlQsivQVhWBE6cCDx4CJll4plUCbT370BppiAGnNqfqKjoAuK5n5k8BFm-ouL1GshiAcBhwu75aHgXGB6lb37nhALB5h4R6R7yD779blaLzLzdmYSMB9nRQIxoJAJuYzzxCdTLzyCB6dSRAACO8QkQS8AAnrOWCiAAuQlJwJkVwDkRWdeeeAYowMfNVskAAA6AbyB-qxCvkR79bJDTkrxAA
