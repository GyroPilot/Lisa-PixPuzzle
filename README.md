# PixPuzzle

> **This repository is retired.** PixPuzzle was the working name. The finished game is
> **Lisa Slide Puzzle 1.0** (the same tool number, 419308):
> https://github.com/GyroPilot/Apple-LisaSlidePuzzle
> Nothing was built here; this repository holds only the first project skeleton.

A photo sliding puzzle for the Apple Lisa Office System: a native LOS
desktop tool that cuts a 680 x 300 one-bit picture into tiles and lets you
slide them back into order. Reuses the Atkinsonpoint .PIX pipeline and
picture packs.

Tool number **419308** in the GyroPilot series (LISACom 419306, Atkinsonpoint
419307, LOS Installer 419310). Written in Lisa Pascal with the Workshop 3.0
toolchain for Lisa Office System 3.1, developed and verified on a Lisa 2/10.

## Status

REV A not started. This repository holds the project skeleton, the build
helpers, and the conventions carried over from LISACom and Atkinsonpoint.
See CHANGELOG.md once builds begin.

## Layout

    sources/PZL-MAIN.TEXT      the program (to come)
    sources/PZL-GLOBALS.TEXT   unit globals: menu constants, panes (to come)
    sources/PZL-ALERTS.TEXT    alerts + menus, Alert tool input (to come)
    sources/PZL-MAKE.TEXT      Workshop exec: compile, link, InstallTool (to come)
    sources/fmt_text.py        REQUIRED for building: converts each source to the
                               Workshop paged .TEXT format (1024-byte header page,
                               no line straddling a 1024 boundary, bare CR line
                               endings). Raw text files will not compile.
    sources/fix_dc42.py        recomputes a DiskCopy 4.2 image's header checksums
    SOURCES.txt                index of what is here and how to build it

## Conventions (from LISACom 1.7 and Atkinsonpoint 1.1)

- Source file names are 8-character identifiers on the Lisa; the PZL- prefix
  keeps this tool's files apart from LMX- (LISACom), SLD- (Atkinsonpoint) and
  INS- (LOS Installer) on a shared Workshop volume.
- Menus are matched to the mi* constants in GLOBALS by position, so MAIN,
  GLOBALS and ALERTS always ship together.
- The linker caps global data at 32K; keep an eye on it from REV A.
- Every source carries a REV header; page-formatted copies sent to the Lisa
  are named with the revision letter (for example PZLMAINA.TEXT).
- Tool icons are a Lisa FONT (chars 0..2, 48x32); a malformed icon file causes
  Level 7 bus errors when the Filer copies the tool. Build icons with
  lisaicon.py from the LISACom kit.
- Pictures are 680 x 300 one-bit .PIX files made with lisapix.py from the
  Atkinsonpoint kit; the starter packs in the AtkinsonPoint repository work
  as-is.
- Floppy masters are written on the 2/10, not the LisaFPGA, and named with
  underscores and one period (for example PIXPUZZLE_1_0.dc42).
