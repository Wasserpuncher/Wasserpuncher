# Kai Pfister

**A claim that nothing checks will eventually be false. So I build the things that check.**

That is not a slogan I picked. I audited the READMEs of my own repositories one night, by hand, and most of them had a number in them that was wrong — several had been wrong since the day they were written, and always in my own favour, which is the direction these errors go. So I stopped trusting prose, including my own, and started writing tools that hold it to the code.

**This page is one of them.** The measured number below is bound, in the Markdown, to the command that produces it, and [a workflow](.github/workflows/profil.yml) re-runs that command on every push and once a week. If the number drifts, this profile goes red. It does not get to quietly stop being true.

### Tools that hold a claim to the truth

**[readme-check](https://github.com/Wasserpuncher/readme-check)** — Runs the console blocks in your README and checks that they still print what you promised. A number in your prose can name the command that settles it, in a comment that renders as nothing. It found the wrong numbers in my own repositories first, and it checks its own README with it.

**[changelog-check](https://github.com/Wasserpuncher/changelog-check)** — Your CHANGELOG cites a commit hash. This checks the commit is actually in your history. The catch is a subtle one: after a rebase the old objects are still lying around, so the obvious test (`git cat-file -e`) passes happily while the entry points at a commit nobody can reach.

**[consent-check](https://github.com/Wasserpuncher/consent-check)** — Your cookie banner claims *"we respect your choice"*. This clicks **Reject all**, then measures what the browser actually does — against the same site's **Accept all** run, so the site is its own yardstick and there is no argument about what counts as a tracker. It reports facts and evidence, never a legal verdict.

**[impressum-check](https://github.com/Wasserpuncher/impressum-check)** — Fails the build when a site is missing a disclosure German law requires (§ 5 DDG, Art. 13 GDPR), and every rule cites the provision it enforces. *Deliberately German: it enforces German law, so its rules and its output speak it.*

**[Layer 8](https://layer8.kaipfstr.de)** — An encyclopedia of real computer, phone and network faults. Its build runs a set of linters over its own content and aborts when a claim is unbacked — a command that would not work, a fix nothing supports. It refuses to publish what it cannot stand behind. *Also deliberately German, because its readers are.*

These belong together. **[The Claim Checkers](https://github.com/Wasserpuncher/the-claim-checkers)** collects them as one family with a single thesis: the gap between what something claims to be and what it is, made measurable, made a build failure.

### Built from scratch

These came first, and they are why the tools above exist: they are the repositories whose READMEs turned out to be lying. No frameworks and no dependencies — the standard library and the problem.

**[rejit](https://github.com/Wasserpuncher/rejit)** — A regular-expression engine (a Pike VM) that matches in guaranteed linear time, so it cannot be ReDoS'd. Against the classic catastrophic pattern `(a+)+$`, Python's `re` multiplies its work about sixteenfold for every four characters of input, while rejit's time does not move at all — that shape is the claim, not any one benchmark. Every CI run cross-checks it against `re` on ten thousand randomly generated pattern/text pairs, asking three questions of each — <!-- readme-check: 30013 = cd .cache/rejit && python -m pytest -q --color=no 2>&1 | grep -oE '[0-9]+ subtests' | grep -oE '[0-9]+' --> 30013 assertions, zero disagreements.

**[tinyjit](https://github.com/Wasserpuncher/tinyjit)** — A JIT compiler in pure Python that writes real x86-64 machine code into executable memory and calls it. No gcc, no LLVM. `55` is `push rbp`, and the CPU runs it directly.

**[x86-disasm](https://github.com/Wasserpuncher/x86-disasm)** — The other half of tinyjit: it turns those bytes back into instructions and is held to GNU objdump's reading of them. One project writes the machine code, the other proves it says what it meant.

**[nanoclone](https://github.com/Wasserpuncher/nanoclone)** — `git clone`, implemented: Smart HTTP v2, packfile delta resolution, a real `.git` index. Every object is verified against its own SHA-1, and real Git sees a clean checkout — `git status` prints nothing.

Also from scratch: [btreedb](https://github.com/Wasserpuncher/btreedb) (an on-disk B+ tree), [tcp-userspace](https://github.com/Wasserpuncher/tcp-userspace) (a TCP/IP stack real `curl` talks to), [cdcl-sat](https://github.com/Wasserpuncher/cdcl-sat) (a SAT solver whose UNSAT answers ship a checkable proof), [minilink](https://github.com/Wasserpuncher/minilink) (a static ELF linker), [deflate-from-scratch](https://github.com/Wasserpuncher/deflate-from-scratch), [recursive-dns](https://github.com/Wasserpuncher/recursive-dns) and [pdb-from-scratch](https://github.com/Wasserpuncher/pdb-from-scratch).

---

Python · Compilers · Networks · Low-level · Würzburg
