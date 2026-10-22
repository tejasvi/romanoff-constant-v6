# New lower bounds for Romanoff's constant (version 6)

Programs and data for the paper *New lower bounds for Romanoff's constant* by Tejasvi Singh Tomar
(doi:10.5281/zenodo.23574562). The programs, the data, a proof of Theorem 1.1 in Lean 4 and two proofs in Lean 4 of
weaker forms of both theorems are archived at doi:10.5281/zenodo.23574563.

Version 6 adds a proof of Theorem 1.1 in Lean 4, in `lean_u3e/`. Version 5 (doi:10.5281/zenodo.23565417) raised the
bound of Theorem 1.2 from 0.118747 to 0.118859, with its certificate, the logs of two checking runs, one at the claimed
bound and one just above it, and the program that wrote the certificate; Theorem 1.2 now uses the modulus of Theorem
1.1. Version 4 (doi:10.5281/zenodo.23557899) raised Theorem 1.1 from 0.110118 to 0.110449 and Theorem 1.2 from 0.118601
to 0.118747, with the checking program that groups the bounds for the singular series by divisors of the period. Version
3 (doi:10.5281/zenodo.23552296) added the checking program of the bounds 0.110118 and 0.118601 and the Lean proof in
`lean_kernel/`, and version 2 (doi:10.5281/zenodo.23548710) the Lean proof in `lean/`. Apart from this README,
`CITATION.cff`, `SHA256SUMS` and the first paragraph of `lean_kernel/README.md`, the files of version 5 are unchanged.

## Results

Let `d` be the lower density of the set of integers `p + 2^a` with `p` prime and `a >= 1`. The paper proves

    d >= 0.110449                                                                  (Theorem 1.1)
    d >= 0.118859, assuming a bound deduced from Lichtman's Theorems 1.2 and 1.7   (Theorem 1.2)

The best lower bound in the literature was 0.10788, from the method of Elsholtz and Schlage-Puchta (Math. Z. 288 (2018),
end of p. 721; recomputed by Johnston and Trudgian, arXiv:2605.17825v2). Theorem 1.2 assumes the bound of Proposition 2
of Johnston and Trudgian, which they deduce from Theorems 1.2 and 1.7 of J. D. Lichtman, arXiv:2309.08522. Both papers
are preprints. Theorem 1.1 uses neither. The Lean proof in `lean_u3e/` proves Theorem 1.1; the two other Lean proofs
prove the bounds `d >= 0.109406` and, under the same assumption, `d >= 0.117953`, which are weaker than Theorems 1.1 and
1.2. In all three the analytic inputs from the literature are hypotheses. Theorem 1.2 is not formalized.

## Method

The integers are split into residue classes modulo an odd squarefree integer `l`. In each class the second moment of the
number of representations is bounded with the per-class sieve bound of Elsholtz and Schlage-Puchta, whose constant 8 is
four times the Hardy-Littlewood prediction. The singular series is bounded with the prime factors of `2^t - 1` for
`t <= 1200` (Section 5 of the paper).

- Theorem 1.1 uses `l = 3*5*7*11*13*17*19*23*31*37*41*73*241`, for which the period of `2^a` modulo `l` is 3960. For
  the part of the singular series that is not computed, only an upper bound for its total is known, not its
  distribution over the divisors of 3960. Bounding Pintz's function in each class from below by one of the linear
  functions of which it is the maximum makes the bound affine in this distribution, so its minimum over all
  distributions is attained at one of 49 extreme ones (Proposition 4.2 of the paper). The checker evaluates the bound
  exactly at all 49.
- Theorem 1.2 uses the same modulus and also bounds the total over all classes with the constant 6.7814 of Johnston and
  Trudgian, through one Lagrange multiplier for the total and one for the caps of each class (Proposition 4.3 of the
  paper).
- The bounds `d >= 0.109406` and `d >= 0.117953` come from a linear program over the distribution of the pair counts
  among the classes, for `l = 3*5*7*11*13*17*31*41*241`, with period 120, and the tail bound `gcd(c, P) theta`. A
  Lagrangian certificate (one multiplier per difference class, Section 4 of the paper) bounds its minimum from below;
  for the first bound all multipliers are zero, so the constant 6.7814 plays no role. The Lean proofs in `lean/` and
  `lean_kernel/` prove these two bounds.

## Contents

| Path | Content |
|---|---|
| `check/check_r45u3e_7e8e7170.py` | the checking program for Theorems 1.1 and 1.2 |
| `check/cert_u3e_23_37_a0644bf2.json` | the certificate of Theorem 1.1 |
| `check/cert_v4e_23_37_5d9c3a60.json` | the certificate of Theorem 1.2 |
| `check/cert_v4d_37e_763ec021.json` | the certificate of version 4 for 0.118747, with the modulus of Theorem 1.1 without the factor 23 |
| `check/cert_u3d_37e_305b0bd9.json`, `check/cert_u3d_perm_2e5fe6fa.json`, `check/cert_u3e_73_f4510070.json`, `check/cert_u3e_41_23_4c20954a.json`, `check/cert_u3e_23_41_64008dfe.json`, `check/cert_u3e_41_aac6e106.json`, `check/cert_u3d_u3x_43bc59a1.json`, `check/cert_v4d_u3x_69a4a859.json` | certificates for the tests below |
| `check/rel2_to_u3e_5800af3a.diff`, `check/u3x_v3_to_u3e_82e5c280.diff` | the changes to this checker from the first checker and from the checker of version 3 |
| `check/check_r45u3x_2cefa154.py` | the checker of version 3, which keeps the bounds for the singular series per residue |
| `check/cert_u3c_73_18aa78b6.json`, `check/cert_v4bb_73_73e5cf24.json` | the certificates of version 3 for 0.110118 and 0.118601 |
| `check/cert_u3b_19_bc628a98.json` | a certificate with the added primes 41 and 19 only (0.109943846) |
| `check/cert_u3x_41_ad7a2738.json`, `check/cert_u3a_c2728dff.json` | the test of the splitting of `l` (below) |
| `check/rel2_to_u3x_cb818175.diff` | the changes from the first checker to the checker of version 3 |
| `check/check_r45a5_rel2_3cf71761.py` | the checking program for the bounds `d >= 0.109406` and `d >= 0.117953` (the first checker) |
| `check/cert_p120b_v3_6fd62e90.json` | the certificate of the bound `d >= 0.117953` |
| `check/cert_p120b_uncond_af1c16be.json` | the certificate of the bound `d >= 0.109406` (all multipliers zero) |
| `check/fac300_41e4cdd6.json` | the complete factorizations of `Phi_t(2)` for `t <= 300` |
| `check/fac1200_fdb_af082adc.json` | factorizations of `Phi_t(2)` for `301 <= t <= 1200` |
| `controls/` | four altered certificates that the checker of Theorems 1.1 and 1.2 rejects, with its output |
| `logs/` | the output of the checking runs and of runs of the floating-point models `scan45d.py` and `scan45e.py`; `logs/review/` holds the runs of an independent review on another machine |
| `reproduce/` | the programs that produced the data and the certificates (not needed for checking) |
| `lean/` | the proof of the bounds `d >= 0.109406` and `d >= 0.117953` in Lean 4, with compiled checks (see `lean/README.md`) |
| `lean_kernel/` | a second proof of the same two bounds in Lean 4, checked by the Lean kernel alone (see `lean_kernel/README.md`) |
| `lean_u3e/` | the proof of Theorem 1.1 in Lean 4, with compiled checks (see `lean_u3e/README.md`) |
| `SHA256SUMS` | the SHA-256 checksums of all other files |

Below, *the main checker* is `check/check_r45u3e_7e8e7170.py`, *the v3 checker* is `check/check_r45u3x_2cefa154.py`,
and *the first checker* is `check/check_r45a5_rel2_3cf71761.py`.

## Checking

The checkers need Python 3 with python-flint (tested with 0.9.0) and numpy. In the directory `check`:

    python3 -I check_r45u3e_7e8e7170.py fac300_41e4cdd6.json cert_u3e_23_37_a0644bf2.json 3000000 fac1200_fdb_af082adc.json 1200 --claim 0.110449 --workers 80
    python3 -I check_r45u3e_7e8e7170.py fac300_41e4cdd6.json cert_v4e_23_37_5d9c3a60.json 3000000 fac1200_fdb_af082adc.json 1200 --claim 0.118859 --workers 42
    python3 -I check_r45a5_rel2_3cf71761.py fac300_41e4cdd6.json cert_p120b_v3_6fd62e90.json 3000000 fac1200_fdb_af082adc.json 1200 --claim 0.117953
    python3 -I check_r45a5_rel2_3cf71761.py fac300_41e4cdd6.json cert_p120b_uncond_af1c16be.json 3000000 fac1200_fdb_af082adc.json 1200 --claim 0.109406

The first run took about 45 minutes with 80 worker processes on a machine with 96 threads
(`logs/u3e_u3e2337_2c4b8603.log`), and the second about 2 hours with 42 on a machine with 44 threads
(`logs/u3e_v4e2337_6eff9e57.log`). The second was also run with `--claim 0.118860` on a second machine
(`logs/u3e_v4e2337_above_7883abe7.log`). The independent review ran both on another machine and printed the same vertex
values (`logs/review/u3e_u3e2337_b436f95f.log`, `logs/review/u3e_v4e2337_d5f14078.log`). The third and fourth runs take
about 29 and 24 minutes, respectively, on one core.
Each run prints the certified value and the value rounded down, and ends with `PASS` and exit code 0 if the certified
value is at least the claim. The line `CERTIFIED` gives the smallest value rounded to the nearest multiple of `1e-9`.
For Theorems 1.1 and 1.2 this rounding goes up: the lines for the vertices show the smallest values to 12 digits,
0.11044979866... and 0.11885963462..., and the line `CERTIFIED` shows both rounded up in the ninth decimal. The line
`rounded down` and the comparison with the claim are exact. With `--claim 0.110450` and `--claim 0.118860` the runs end
with `FAIL` and exit code 1 (`logs/review/u3e_u3e2337_above_c735e7cc.log`, `logs/u3e_v4e2337_above_7883abe7.log`,
`logs/review/u3e_v4e2337_above_db187433.log`).
`3000000` is the bound at which the dynamic program over the orders stops a branch, and `1200` is the largest order of 2
modulo the primes of class (b) (Section 5 of the paper). Without the arguments `fac1200_fdb_af082adc.json 1200` the
checkers leave out class (b) and certify smaller values.

The first checker recomputes everything from the factorization files and the
certificate:
- It checks by multiplication that the factorizations for `t <= 300` are complete and proves every factor prime. For
  `301 <= t <= 1200` it checks the products and proves the primality and the order `t` of every factor below `10^100`
  that is coprime to `t`. It does not use the other factors.
- It computes the orders exactly, bounds the singular series in ball arithmetic and, for class (b), in floating point with
  outward rounding and a relative margin of `1e-9`.
- It builds the residue patterns and their rotation orbits and evaluates the Lagrangian bound in exact rational arithmetic.

The certificate contains the prime factors of `l`, the multipliers and the external constants: the per-class constant 8,
the total constant 6.7814, `C0 < 0.66016181584686958` for the twin prime constant `C0`,
`0.693147180559945309 < log 2 < 0.693147180559945310` and `R0 < 1.93656` for the sum (2.3) of the paper. In the
certificate of the bound `d >= 0.109406` the total constant is 8; it has no effect there, since all multipliers are zero.
The checker requires:
- the per-class constant to be at least 8 and the total constant at least 6.7814, both at most 100;
- `0.66016181584686958 <= C0_up <= 1`, `0.6931471805599453 <= log2_low <= 0.693147180559945309`,
  `0.693147180559945310 <= log2_up <= 0.6931471805599454` and `1.93656 <= R0_up <= 2`;
- the prime factors of `l` to be distinct odd primes, and the primes in each factorization to be distinct;
- the multipliers to be nonnegative.

It prints all parameters in its first line, and as a precaution it refuses to run under `python -O`.

The main checker contains the code of the first checker unchanged for the factorizations and the
external constants. For the bounds for the singular series it uses the dynamic program and the class-(b) sums of the
first checker, but adds them up per divisor of the period instead of per residue; `rel2_to_u3e_5800af3a.diff` lists every
change. From the v3 checker it keeps the code for the patterns, the orbits, the Pintz indices and the
vertices; `u3x_v3_to_u3e_82e5c280.diff` lists the changes. For a certificate of format `r45a-u3e` it evaluates the bound
of Proposition 4.2 of the paper:
- It splits `l` into `l' = 3*5*7*11*13*17*31*241` and the added primes, 41, 19, 73, 23 and 37 for both theorems. It
  enumerates the residue patterns modulo `l'` and the 7,870 rotation orbits of the nonempty ones, combines each orbit
  with all residues modulo the added primes, and checks that the class counts add up to `l` (Section 6 of the paper).
- It groups the bounds for the singular series of classes (a) and (b) by the divisors `g` of the period: `T_0(c)` is the
  sum of the numbers `B_g` over the `g` that divide `c` (Section 5 of the paper), each `B_g` rounded up to a multiple of
  `2^-48`; the bounds for the branches that the dynamic program stops go into `B_1`. For each combination it computes
  the size of the pattern, the sums `S_g` and `Q = sum_g B_g S_g` of Proposition 4.2 exactly in integers. The residues
  modulo the last added prime, 37, are evaluated together from the counts of one pattern in the classes modulo the
  divisors of the period.
- It chooses the Pintz index of each combination in floating point, at the point given by the certificate's field
  `alpha_j`. This choice affects only how good the bound is.
- It evaluates the bound at all vertices of the simplex, 49 for the period 3960 and 25 for 360, in exact rational
  arithmetic, prints all values and certifies the smallest.

Besides the checks of the first checker, it requires the tail mode `alpha_simplex`, no multipliers per difference class
(the field `duals` of the first checker), the added primes to be distinct prime factors of `l` and `l'` to be nonempty,
the number of orbits to match the certificate, the point `alpha_j` to lie in the simplex, on divisors of the period,
Pintz indices at least 1, and integer bounds under which all its int32 and int64 arithmetic is exact. It starts its
worker processes with `fork`, which needs Linux or macOS. The certificate of Theorem 1.2 and
`cert_v4d_37e_763ec021.json` have a field `mu`, the multiplier of Proposition 4.3 of the paper, which must be
nonnegative, and the total constant 6.7814; the checker then evaluates the bound of Proposition 4.3 in the same way. The
other certificates of format `r45a-u3e` here have no such field, so the total bound is not used, and their total
constant 8 has no effect.

The main checker was tested in three ways (Section 6 of the paper):
- `cert_u3e_73_f4510070.json` is the certificate `cert_u3c_73_18aa78b6.json` of version 3 (the modulus
  `3*5*7*11*13*17*19*31*41*73*241`, period 360) in the format `r45a-u3e`. The checker certifies 0.110118630 for it
  (`--claim 0.110118`), as the v3 checker does for `cert_u3c_73_18aa78b6.json`. Of the 25 vertex values, 24
  agree in all 12 printed digits; the value at `e_72` differs by `1e-12`, since the main checker rounds on the grid
  `2^-48` and the v3 checker on the grid `2^-40` (`logs/review/u3e_u3e73_9b11f98b.log`,
  `logs/u3x_u3c73_6c56e930.log`). For the modulus of Theorem 1.1 without the factor 23, `cert_u3d_u3x_43bc59a1.json`
  and `cert_v4d_u3x_69a4a859.json` are `cert_u3d_37e_305b0bd9.json` and `cert_v4d_37e_763ec021.json` with the format
  changed to `r45a-u3x` (their fields `note` are copied unchanged). The v3 checker, which evaluates every
  exclusion at every added prime separately, certifies them with `--claim 0.110277` and `--claim 0.118747`, with the
  same smallest vertex values 0.110277417054 and 0.118747326926 as the main checker. All 25 vertex
  values agree for `cert_v4d_37e`, and 23 for the other, whose values at `e_8` and `e_45` differ by
  `1e-12` (`logs/review/u3x_u3d37_878419da.log`, `logs/review/u3x_v4d37_754e23b3.log`; about 2.2 and 2.4 hours with 48
  worker processes).
- `cert_u3d_37e_305b0bd9.json` and `cert_v4d_37e_763ec021.json` are the unconditional and the conditional certificate
  for the modulus of Theorem 1.1 without the factor 23; the checker certifies 0.110277417 and 0.118747326 for them
  (`--claim 0.110277` and `--claim 0.118747`; `logs/u3e_u3d37_0e81d689.log`, `logs/u3e_v4d37_8ebad28f.log`). The
  review's runs of `cert_v4d_37e` are `logs/review/u3e_v4d37_30fec38c.log` and, with `--claim 0.118748` (`FAIL`),
  `logs/review/u3e_v4d37_above_cdd7c1b1.log`. `cert_u3d_perm_2e5fe6fa.json` is `cert_u3d_37e_305b0bd9.json` with the
  added primes in the order 41, 19, 37, 73, so that 73 instead of 37 is evaluated as the last added prime; its field
  `note` is copied unchanged. In the review `cert_u3d_37e` and `cert_u3d_perm` gave the same 25 vertex values, in all 12
  digits (`logs/review/u3e_u3d37_e38cf6e6.log`, `logs/review/u3e_u3d37perm_5338ef8d.log`). Likewise,
  `cert_u3e_41_23_4c20954a.json` and `cert_u3e_23_41_64008dfe.json` use the added primes 41 and 23, with period 1320,
  and differ only in which of the two is last; both certify 0.109834575 (`--claim 0.109834`), and the 33 vertex values
  agree in all 12 digits (`logs/u3e_u3e4123_6b24f0d0.log`, `logs/u3e_u3e2341_5a7ff866.log`; about 3 minutes each with
  one worker process).
- The test of the splitting of `l`, described below.

The directory `controls/` holds four certificates derived from `cert_u3e_73_f4510070.json` and the output of the checker
on them. Each run ends with `FAIL` and exit code 1: `alpha_mass` puts 1.001 times the allowed mass on the point `alpha_j`,
`add_not_in_ell` lists an added prime that does not divide `l`, `orbits` states 7,871 instead of 7,870 orbits, and
`wrong_vertex` chooses the Pintz indices at the vertex `e_1` and claims 0.110173, while the smallest vertex value is then
0.11011862659.

The splitting of `l` into `l'` and the added primes is tested, for one added prime and without a change of period, on
the modulus `3*5*7*11*13*17*31*41*241` of the bound `d >= 0.109406`, with period 120. `cert_u3x_41_ad7a2738.json` splits
off the prime 41, and `cert_u3a_c2728dff.json` (format `r45a-u3`) runs through the 92,206 rotation orbits of the full
patterns, as the first checker does. With the v3 checker both certify 0.109618905 (`--claim 0.109618`), and the
17 values printed for the vertices agree in all 12 digits (`logs/u3x_u3x41_3bab4a50.log`, `logs/u3x_u3a_c6c2b1f4.log`).
For `cert_u3e_41_aac6e106.json`, which is `cert_u3x_41_ad7a2738.json` in the format `r45a-u3e`, the checker of Theorems
1.1 and 1.2 gives the same 17 values (`logs/u3e_u3e41_3a5dba29.log`).
The v3 checker certifies 0.110118630 for `cert_u3c_73_18aa78b6.json` and 0.118601142 for
`cert_v4bb_73_73e5cf24.json` (`logs/u3x_u3c73_6c56e930.log`, `logs/u3x_v4bb73_7a2c56b2.log`).

## Formal proofs in Lean

The directory `lean/` contains a proof of the bounds `d >= 0.109406` and, under the bound (2.2), `d >= 0.117953` in Lean
4 (version v4.35.0-rc3) with Mathlib (commit c55e6e786f49): the theorems `Romanoff.romanoff_U2` and
`Romanoff.romanoff_v3` in `lean/Romanoff/Theorems.lean`. They are weaker than Theorems 1.1 and 1.2. The analytic inputs
of Section 2 of the paper are the hypotheses of these theorems: the per-class bound (2.1) for the modulus `l =
3*5*7*11*13*17*31*41*241`, the prime number theorem in progressions modulo `l` and the bound (2.3) for `R0`, stated for
its finite partial sums, and for the second bound also the bound (2.2) for the total. Pintz's inequality (Lemma 2.1) is
proved. The checks of the data run as compiled code through `native_decide`, so `#print axioms` lists the three standard
axioms and four auxiliary axioms for each theorem (`lean/results/axioms_shipped.txt`). `lean/README.md` describes the
files and gives the build commands.

The directory `lean_kernel/` contains a second proof, a separate Lake project in which no module uses `native_decide`:
the theorems `Romanoff.romanoff_U2_K` and `Romanoff.romanoff_v3_K` in `lean_kernel/Romanoff/CertKFinal.lean` have the
same statements and hypotheses, and each depends only on the three standard axioms
(`lean_kernel/results/axioms_shipped.txt`). The computations are split into theorems that the kernel checks by
evaluation: 244 for the list of primes, the lower sums for `R0` and the bounds `T+(c)`, and 185 for the Lagrangian
bound, with the 92,206 rotation orbits computed by a fold whose steps the kernel checks. `lean_kernel/README.md`
describes the files and gives the build and regeneration commands; the build took 1 h 35 min, not counting Mathlib, on
one machine with 32 threads and 128 GB of memory.

The directory `lean_u3e/` contains a proof of Theorem 1.1, a separate Lake project with the same Lean and Mathlib
versions: the theorem `Romanoff.E.romanoff_U3e` in `lean_u3e/Romanoff/E/U3e.lean` states `0.110449 <= liminf d_N`, where
`d_N` is the proportion of the integers `1 <= n <= N` of the form `p + 2^a`. Its hypotheses are the per-class bound
(2.1) and the prime number theorem in progressions for the modulus of Theorem 1.1, and the bound (2.3) for `R0`, stated
as for the other proofs. Six computations run as compiled code through `native_decide`: five checks of the data and of
the bounds for the singular series, and the evaluation of the bound by a program written in Lean, which follows the main
checker. So `#print axioms` lists the three standard axioms and six auxiliary axioms
(`lean_u3e/results/axioms_shipped.txt`). The exported proof was accepted by `leanchecker`, which runs Lean's kernel, and
by two further implementations of the Lean kernel, nanoda and lean4lean, with the six auxiliary axioms admitted. The
program obtains the value 0.1104501353..., a little above the checker's smallest value, because its bounds for the
singular series spread the contribution of the branches that the dynamic program stops over the divisors of the period;
`lean_u3e/README.md` explains the difference, describes the files and gives the build commands (the evaluation takes
about 50 minutes on 90 cores).

## Reproduction

The programs in `reproduce/` produced the data and the certificates. Their names, like those of the data files, end with
the first eight hex digits of the file's SHA-256. To run them, copy them to names without this suffix
(`dual_opt.py` imports `patterns_fast`). They need python-flint, numpy and highspy.
- `fetch_fdb.sh` and `fdb_to_phi.py` fetch the factorizations of `2^t - 1` from factordb and convert them to
  factorizations of `Phi_t(2)`; `factor_full.py` factors `Phi_t(2)` for `t <= 300` with FLINT; `verify_factors.py`
  checks the files.
- `patterns_fast.py` computes the residue patterns and their orbits, and `dual_opt.py` computes the multipliers from
  the parameter file `params_p120b_e724da74.json` and the singular-series bounds `tails_p120b_v5_c073e0de.json` (which
  the checker recomputes).
- `cert_build3.py` solves the linear program in floating point with HiGHS, as a cross-check of the multipliers.
- `sensitivity.py` evaluates the Lagrangian bound in floating point, with one common multiplier, for other values of
  the two constants; `sens_p120b_a87b7f38.log` is its output for the modulus `3*5*7*11*13*17*31*41*241`. These values
  are not certified, and the checker refuses most of these constants.
- From the certificate of the bound `d >= 0.109406`, `make_u3_certs.py` writes the certificate `cert_u3c_73` of version 3,
  the certificate with the added primes 41 and 19, and the two certificates of the splitting test:
  `python3 -I make_u3_certs.py ../check/cert_p120b_uncond_af1c16be.json OUTDIR`.
  These certificates contain only parameters: the checkers recompute the number of orbits and require it to match, and
  the point `alpha_j` affects only how good the bound is.
- `make_u3de_certs.py` writes the certificate of Theorem 1.1, `cert_v4d_37e`, `cert_u3d_37e`, `cert_u3e_73` and the
  four certificates in `controls/` into the output directory of `make_u3_certs.py`: `python3 -I make_u3de_certs.py
  OUTDIR`. For `cert_v4d_37e` the only new data are the total constant 6.7814 and the multiplier `mu = t nu` (with `nu`
  as in Section 4 of the paper), rounded to `10^-12`, with the value `t = 3.676e-3` chosen for version 3.
  `cert_u3d_perm` is `cert_u3d_37e` with the order of the added primes changed, and `cert_u3d_u3x` and `cert_v4d_u3x`
  are `cert_u3d_37e` and `cert_v4d_37e` with the field `format` changed to `r45a-u3x`; no program here writes these
  three files.
- `make_v4e_cert.py` writes the certificate of Theorem 1.2 from the certificate of Theorem 1.1 in `OUTDIR` (the output
  directory of `make_u3de_certs.py`), by the same rule: `python3 -I make_v4e_cert.py OUTDIR`.
- `make_u3e_tests.py` writes the test certificates `cert_u3e_41`, `cert_u3e_41_23` and `cert_u3e_23_41` from
  `cert_u3x_41`: `python3 -I make_u3e_tests.py ../check/cert_u3x_41_ad7a2738.json OUTDIR`.
- `make_v4_certs.py` writes the certificate `cert_v4bb_73` of version 3 from `cert_u3c_73`:
  `python3 -I make_v4_certs.py DIR`, with `DIR` the output directory of `make_u3_certs.py`.
  It also writes three other conditional certificates, which are not used here. The only new data are the total
  constant 6.7814 and the multiplier `mu = t nu`, rounded to `10^-10`, with `t = 3.676e-3`; of the three values of `t`
  that were tried with the checker, this one gave the largest bound.
- `scan45e.py` is the floating-point model of the bound of Proposition 4.3 with which `t` was chosen. It divides by
  the number of classes with nonempty patterns instead of `l`, so its printed bounds are about `1e-6` too high, but
  the best `t` is the same. Its run for the added primes 41 and 19, and 41, 19 and 73, is `logs/scan45e_e2929b18.log`;
  for 41, 19 and 73 it gives 0.118602159 at `t = 3.676e-3`.
- `scan45b.py`, `scan45c.py` and `scan45d.py` are floating-point models of the bound with which the added primes and the
  point `alpha_j` were chosen; the runs that chose the added primes 23 and 37, each of which adds one candidate prime
  `q` to 41 (the modulus `l'*41*q`), are not included. They take class (b) from the factorization file without primality
  proofs, so they certify nothing. `scan45b.py` evaluates the bound with the tail bound `gcd(c, P) theta` of Section 5
  for candidate added primes, `scan45c.py` searches the simplex of Proposition 4.2 for its worst point, and `scan45d.py`
  evaluates the bound of Proposition 4.2 for candidate added primes. The command
  `python3 -I scan45d.py ../check/fac300_41e4cdd6.json ../check/fac1200_fdb_af082adc.json 3,5,7,11,13,17,31,241 41,19 73`
  prints 0.109943846 for the added primes 41 and 19 and 0.110118630 for 41, 19 and 73; its output is
  `logs/scan45d_ba953f7e.log` (10 minutes on one core, 20 GB of memory). The usage lines of all four scan programs say
  `scan45b.py`, and the docstring of `scan45e.py` still describes the unconditional bound.

## Notes

- The `note` fields inside the certificates of the bounds `d >= 0.117953` and `d >= 0.109406` were written for the
  earlier checker `check_r45a5_rel_ab861be2.py` and name the certificates without the hash suffix. The checker here
  supersedes that one: it adds the input checks listed above and certifies the same values.
- The notes call the inputs (I1) to (I5): (I1) is the per-class bound (2.1) of the paper, (I2) the total bound (2.2),
  (I3) the prime number theorem in progressions, (I4) Lemma 2.1 and (I5) the bound (2.3) for `R0`.
- The docstrings and the `note` fields of the files for the two theorems use these names: `U2` for the bound
  `d >= 0.109406`; `U3a` for the same modulus with the tail of Proposition 4.2 (0.109618905); `BASE` for the factor `l'`
  and `ADD` for the added primes; in the `note` fields, `U3b` and `U3c` for the certificates with the added primes 41
  and 19, and 41, 19 and 73 (the docstrings of `make_u3_certs.py` and `make_u3de_certs.py` use `U3b` for the stage of
  version 3 that includes both); `V4bb` for the certificate `cert_v4bb_73`; `U3e` and `V4e` for the certificates of
  Theorems 1.1 and 1.2 (`V4e` is the conditional form of `U3e`); `V4d` for `cert_v4d_37e`, the conditional form of `U3d`,
  the certificate `cert_u3d_37e`; and "divisor form" for the grouping of the bounds by divisors of the period.
- The certificates of version 3 were first checked with an earlier revision of the v3 checker (SHA-256
  `b90c40dd77e6824d…`). It required `PER <= 4096` for its int64 arithmetic, which is too weak in general (it needs
  `PER < 1448`) but holds for `PER = 360`. The shipped revision requires `PER^2 max(Tg) < 2^63` for the grid integers
  `Tg = ceil(T 2^40)` instead, bounds the weighted row sums of every orbit, and sums the row weights as a Python integer.
  These are its only changes, and both revisions certify the same values.
- The parameter notes attribute `R0 < 1.93656` to Khalfalah and Pintz. The bound follows from Pintz's
  `C0 R0 < 1.2784421041` (Acta Math. Hungar. 112 (2006), Lemma 2'') and `C0 > 0.6601618158`, as quoted by Platt and
  Trudgian (J. Number Theory 153 (2015), p. 55).

## License

Apache License 2.0, see `LICENSE`.
