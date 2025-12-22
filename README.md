# Black-Box On-Policy Distillation of Large Language Models

This repository contains the algorithm implementation for our paper **"Black-Box On-Policy Distillation of Large Language Models"**.

📄 **Paper**: [arXiv:2511.10643](https://arxiv.org/abs/2511.10643)

💾 **Data**: [LMSYS-Chat-GPT-5-Chat-Response](https://huggingface.co/datasets/ytz20/LMSYS-Chat-GPT-5-Chat-Response)

🤖 **Models**: [GAD Models](https://huggingface.co/collections/ytz20/gad-models)

## 🚀 Getting Started

We use two repos as to easily install different branches for different experiments. Check [GAD Repo](https://github.com/microsoft/LMOps/tree/main/gad) for environment setup and scripts for running experiments. Check this repo for algorithm implementation. 

We implement based on [VeRL](https://github.com/volcengine/verl). **We hack to use the `critic` module in VeRL as our discriminator**.

There are four branches in this repo: `seqkd` branch for running the SeqKD baseline, `warmup` branch for warmup stage of our method, `gad` branch for GAD training stage of our method and `eval` branch to use the already-trained model to perform generation only.

For SeqKD and warmup stage of GAD, the student is supervised-finetuned on the teacher response (corresponding code at [sft_seqkd](https://github.com/YTianZHU/verl/blob/seqkd/verl/workers/actor/dp_actor.py#L485) and [sft_warmup](https://github.com/YTianZHU/verl/blob/warmup/verl/workers/actor/dp_actor.py#L495)). We choose to use this VeRL-based repo to implement them for best alignment.

### Code Guide

We provide a code walk-through of this branch `seqkd`. You can also use other codebases to perform supervised-finetuning on teacher responses.

- [Training Entrance](https://github.com/YTianZHU/verl/blob/seqkd/verl/trainer/ppo/ray_trainer.py#L957)
- Process on Teacher Data: [Entrance](https://github.com/YTianZHU/verl/blob/seqkd/verl/trainer/ppo/ray_trainer.py#L1035) and [Implementation](https://github.com/YTianZHU/verl/blob/seqkd/verl/workers/rollout/vllm_rollout/vllm_rollout_spmd.py#L257)
- SFT Student on Teacher Response: [Entrance](https://github.com/YTianZHU/verl/blob/seqkd/verl/trainer/ppo/ray_trainer.py#L1083) and [Implementation](https://github.com/YTianZHU/verl/blob/seqkd/verl/workers/actor/dp_actor.py#L523)


## 📄 Citation

If you find this work useful, please cite our paper:

```bibtex
@article{ye2025blackboxonpolicydistillationlarge,
  title={Black-Box On-Policy Distillation of Large Language Models},
  author={Tianzhu Ye and Li Dong and Zewen Chi and Xun Wu and Shaohan Huang and Furu Wei},
  journal={arXiv preprint arXiv:2511.10643},
  year={2025},
  url={https://arxiv.org/abs/2511.10643}
}
```

## 📧 Contact

For any questions or issues, please open an issue in this repository.