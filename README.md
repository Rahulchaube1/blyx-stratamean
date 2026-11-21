<img src="assets/logo.png" width="112" height="112" alt="StrataMean logo">

# StrataMean

Pool event counts and expose the crude observed rate. This Blyx library is part of the probability and causal analysis collection.

A change in the mix of observed groups can move the pooled rate. Recalculate rates against fixed reference weights before comparing populations. [NCI SEER, direct age adjustment](https://seer.cancer.gov/seerstat/tutorials/aarates/definition.html)

## Install and run

Install [Blyx 0.2.1](https://www.blyx-lang.space/download) with a Rust toolchain and host linker for native builds.

```sh
git clone --depth 1 --branch v0.1.1 https://github.com/Rahulchaube1/blyx-stratamean.git
cd blyx-stratamean
blyxc native-run example.blyx
blyxc native-run tests.blyx
```

[Run the editable browser example](https://www.blyx-lang.space/play?example=package-stratamean) · [Package page](https://www.blyx-lang.space/packages/stratamean) · [Handbook](https://doc.blyx-lang.space/guide/jacana)

## Import the module

Run this in the directory containing your application's entry file.

```sh
git clone --depth 1 --branch v0.1.1 https://github.com/Rahulchaube1/blyx-stratamean.git vendor/stratamean
```

```blyx
use vendor::stratamean::stratamean;

fn main() {
    let events = [2, 6];
    let trials = [4, 8];
    let result = stratamean_pooled(events, trials);
    if len(result) == 0 { println!("invalid"); return; }
    let mut i = 0;
    while i < len(result) {
        println!(at(result, i));
        i += 1;
    }
}
```

Expected output

```text
8
12
0.6666666666666666
```

## API

`stratamean_pooled(events, trials)`

Returns [total events, total trials, crude rate]. Every stratum must have observations and events cannot exceed trials. Invalid arguments and nonfinite results return an empty vector. Integers carried in numeric vectors use the exact range from −(2^53−1) to 2^53−1.

| Argument | Domain |
| --- | --- |
| events | Vector of values, each a nonnegative exact integer |
| trials | Vector of values, each a nonnegative exact integer |

## In use

[Jacana](https://github.com/Rahulchaube1/blyx-jacana) uses this module to compare a crude event rate with a directly standardized rate.

## Verification and contributions

The regression suite in [tests.blyx](tests.blyx) checks the example, boundary cases and invalid inputs. Include a short reproducer and your compiler version in [an issue](https://github.com/Rahulchaube1/blyx-stratamean/issues). The source is dual-licensed under [MIT](LICENSE-MIT) or [Apache-2.0](LICENSE-APACHE). The package artwork uses [Lucide icons](https://lucide.dev/license); see [artwork notices](assets/NOTICE.txt).

## Connect with Rahul Chaube

[Portfolio](https://www.rahulchaube1.com/) · [GitHub](https://github.com/Rahulchaube1) · [LinkedIn](https://www.linkedin.com/in/rahulchaube1) · [Hugging Face](https://huggingface.co/oncody) · [X](https://x.com/RahulChaube_) · [EverestQ](https://www.everestqai.com/) · [Contact](https://www.rahulchaube1.com/contact)

[Blyx website](https://www.blyx-lang.space/) · [BlyxTorch](https://www.blyx-lang.space/packages/blyxtorch) · [Handbook](https://doc.blyx-lang.space/) · [Community](https://www.blyx-lang.space/community)

Support Rahul’s open-source work through [GitHub Sponsors](https://github.com/sponsors/Rahulchaube1) or [Buy Me a Coffee](https://buymeacoffee.com/rahulchaube).
