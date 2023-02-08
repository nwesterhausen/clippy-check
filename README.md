<p align="center">
  <a href="https://github.com/actions/typescript-action/actions"><img alt="typescript-action status" src="https://github.com/actions/typescript-action/workflows/build-test/badge.svg"></a>
</p>

# clippy check

Started from the `actions/typescript-actions` template :rocket:

See the actions-rs [clippy-check](https://github.com/actions-rs/clippy-check) (which isn't [maintained](https://github.com/actions-rs/clippy-check/issues/162)).

Code actually hefted from [LoliGothick/clippy-check](https://github.com/LoliGothick/clippy-check) because that action was not working due to the dist/ dir being out of date. (Originally I had forked it but ultimately decided it would be better to use the typescript-actions preset tooling and just copied the typescript code over.)

So with this repo being based on the typescript-actions template and having updated toolchaining, it hopefully can be maintained and run well.

## Example workflow

```yml
clippy:
    name: clippy check
    runs-on: ubuntu-latest
    steps:
        - uses: actions/checkout@v2
        - uses: actions-rs/toolchain@v1
          with:
              toolchain: nightly
              components: clippy
              override: true
        - uses: nwesterhausen/clippy-check@v1
          with:
              token: ${{ secrets.GITHUB_TOKEN }}
              allow: >
                nonstandard_macro_braces
                mutex_atomic
              deny: warnings  
```

## Inputs

|  Name   | Required | Description                                                                                                                             |  Type  |         Default         |
| :-----: | :------: | :-------------------------------------------------------------------------------------------------------------------------------------- | :----: | :---------------------: |
|  token  |    ✔    | GitHub secret token, usually a `${{ secrets.GITHUB_TOKEN }}`.                                                                           | string |                         |
| options |          | Options for the `cargo calippy` command.<br>`--message-format=json` is set by default.<br>Given `--message-format` is omitted silently. | string | `--message-format=json` |
|  warn   |          | Sequence for lint warnings (without `clippy::`).                                                                                        | string |                         |
|  allow  |          | Sequence for lint allowed (without `clippy::`).                                                                                         | string |                         |
|  deny   |          | Sequence for lint denied (without `clippy::`).                                                                                          | string |                         |
| forbid  |          | Sequence for lint forbidden (without `clippy::`).                                                                                       | string |                         |
|  name   |          | Name of the created GitHub check. If running this action multiple times, each run must have a unique name.                              | string |         clippy          |
