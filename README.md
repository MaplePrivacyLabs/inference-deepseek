# Maple DeepSeek inference configuration

Tinfoil Containers configuration for **DeepSeek-V4.1-Flash-1017** on four
NVIDIA B300 GPUs. This repository publishes the measured deployment configuration;
it reuses Tinfoil's digest-pinned inference image and verified model pack.

## Upstream provenance

`tinfoil-config.yml` derives from
[tinfoilsh/confidential-deepseek-v4-1-flash v0.0.6+b300](https://github.com/tinfoilsh/confidential-deepseek-v4-1-flash/tree/v0.0.6%2Bb300),
commit `28775a51ed83ddd1cd295852db46499d7d50c480`.

- Model: `deepseek-ai/DeepSeek-V4.1-Flash-1017`
- Model revision: `1bae0e1088993b9b82de08f59de5be5a34e42170`
- Image digest: `sha256:01dae35f82bd4fb13376a9d1f0330e4109c1c03a07532f8df3bb12f9b0e58880`
- Resources: four GPUs, 56 CPUs, 768 GiB RAM; tensor parallelism four.
- Confidential VM image: `0.14.13`; verified model-pack schema: `2`.
- Authentication: native vLLM bearer authentication with required `VLLM_API_KEY`;
  the CVM metrics handlers use required `METRICS_API_KEY`. Secret values are
  deployment settings. The upstream `/tokenize` and `/metrics` paths are omitted.

The release workflows derive from
[Tinfoil's container template](https://github.com/tinfoilsh/tinfoil-containers-template/tree/0eddc320b8f328d7a3c057152596934444ac2d75/.github/workflows).
The measurement action is pinned to the same `v0.14.0` commit used by the
upstream DeepSeek release. These workflows do not rebuild or publish an inference
image.

## Publish a configuration release

Run **Tinfoil Release** with a new version such as `v0.1.0`. It creates the
source tag, dispatches the publish workflow on that tag, measures the configuration,
and publishes the release and attestation under this repository's identity.
Wait for both workflow phases and the published release before selecting it in
Tinfoil Containers.

Instance names, target hosts and custom domains are deployment settings. API keys
and other credential values must remain outside this public repository.

The model's license is maintained by
[DeepSeek](https://huggingface.co/deepseek-ai/DeepSeek-V4.1-Flash-1017/blob/1bae0e1088993b9b82de08f59de5be5a34e42170/LICENSE).
See the linked upstream repositories for their source and notices.
