# Contributing to nothing-phone-bootloop-recovery

## What this repo is

This repo is the written record of one completed repair: a Nothing Phone (3a)
that was stuck in a boot loop after a rooting attempt and was restored by
flashing a single stock boot image. There is no application code here. The
repo is documentation, and its only value is accuracy.

## How to report a problem

Open an issue on GitHub. Say what you were doing, what you expected, and what
happened instead. If the report is about this record rather than about your
device, point at the file and line. Command output and screenshots are welcome.

Reports about your own device are not part of this repo. If your phone is
looping, follow the reproduce steps in the README and confirm every detail
against your own build before flashing anything. Never flash anything based on
a checksum you have not verified yourself.

## How to submit a change

1. Fork the repository.
2. Create a branch off `main` for your change. Name it after the change, for
   example `fix-typo` or `add-slot-warning`.
3. Make your edits on that branch.
4. Open a pull request back to `main`, and describe what you changed and why.

Small, focused pull requests are easier to review than large ones. Keep one
pull request per topic.

## Accuracy rules

These rules are not optional. They exist because the entire point of this repo
is to be a trustworthy record.

- All numbers, checksums, and command outputs must come from the real files.
  Never invent a checksum, a size, a build number, or a log line.
- Every claim about the procedure must be backed by the `recovery-completed.md`
  record. If it is not in that record, it did not happen here.
- The staged image checksums in this repo are SHA-256 values verified against
  the build archive `Asteroids_V3.2-251013-1406`. Treat them as facts, not as
  values to guess at.
- If you observe something different on your own device, add it as a separate,
  clearly labeled section. Do not edit the original record to match your case.
- When in doubt, cite the file and line. A claim with a pointer beats a claim
  with a memory.
