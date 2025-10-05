
```
RUSTFLAGS="-Z autodiff=Enable,NoTT,PrintModBefore" cargo +enzyme rustc --release --lib --crate-type=staticlib &> mod_after_o3.ll
```

```
RUSTFLAGS="-Z autodiff=Enable,NoTT,PrintModBefore -C no-prepopulate-passes" cargo +enzyme rustc --release --lib --crate-type=staticlib &> mod_no_passes_run.ll
```

The previous two commands fail, however if we take the IR before we ran enzyme and manually run libEnzyme via opt, it succeeds:

```
~/prog/rust2/build/x86_64-unknown-linux-gnu/llvm/build/bin/opt mod.ll -load-pass-plugin=/home/manuel/prog/rust2/build/x86_64-unknown-linux-gnu/stage1/lib/libEnzyme-21.so -passes="enzyme" -o rel3.ll -debug-pass-manager -S
```


