# baselinedmypy_mypyc-wheels
Automated building and storage of mypyc-compiled mypy binaries

Note: this is an experimental fork of [mypyc/mypy_mypyc-wheels](https://github.com/mypyc/mypy_mypyc-wheels/) 
for building wheels for [BaselinedMypy](https://github.com/Zeckie/baselinedmypy/)

![Build wheels status](https://github.com/Zeckie/baselinedmypy_mypyc-wheels/workflows/Build%20wheels/badge.svg)

## Things to know

If you're running into weird issues with a pull request, try updating the
`mypy_commit` file to the latest hash from the mypy repo.

If wheels aren't getting built, debug over at
https://github.com/Zeckie/baselinedmypy_mypyc-wheels/actions

You can use pip to install these wheels like so:
```
pip install --upgrade --find-links https://github.com/Zeckie/baselinedmypy_mypyc-wheels/releases/tag/v0.920+dev.48181d26e7575aece8cab61eb866ac6c573dfd76 mypy
# or possibly
pip install --upgrade --find-links https://github.com/Zeckie/baselinedmypy_mypyc-wheels/releases/latest mypy
```

##  Building locally

With [pipx](https://pipx.pypa.io) installed, run:

```bash
COMMIT=$(cat mypy_commit)
git clone https://github.com/Zeckie/baselinedmypy.git --recurse-submodules
(cd mypy && git checkout $COMMIT)
pipx run cibuildwheel --config=cibuildwheel.toml mypy
```

Optionally add `--only=<identifier>` to build only one wheel, or set
`CIBW_BUILD` to some expression like `cp311-*` and include `--platform linux`
(or some other platform). Optionally pin cibuildwheel to the version specified
in `.github/workflows/build.yml`.
