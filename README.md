# Traditional-Chinese Alpaca Dataset

This repo aims to share resources for building Traditional-Chinese instruction-following language models (for research purposes only). This repo contains:
  - A Traditional-Chinese version of the Alpaca dataset with English alignment. See [Dataset](#dataset) for details. Our *very simple* alignment technique could work for other languages as well.
  - Code for training and inferencing the Traditional-Chinese Alpaca-Lora LLaMA model.
  
## Dataset <a name="dataset"></a>
We translate the [Stanford Alpaca 52k dataset](https://github.com/tatsu-lab/stanford_alpaca/blob/main/alpaca_data.json) directly to Traditional Chinese via the [ChatGPT API](https://platform.openai.com/docs/guides/chat) (```gpt-3.5-turbo```), which cost us roughly 40 USD.

Specifically, this repo includes three set of datasets:
1.  A Traditional-Chinese version of the Alpaca dataset. --> [```alpaca_data-tw.json```](alpaca_data-tw.json)
2.  A dataste same as 1. except the *instruction part* is leaved as English. --> [```alpaca-tw_en_instruction.json```](alpaca-tw_en_instruction.json)
3.  A dataset combining 1. and 2. --> [```alpaca-tw_en-align.json```](alpaca-tw_en-align.json)

In our preliminary experiments, fine-tuned only with dataset 1. does not yield ideal results.
As LLaMA is trained primarily on English corpus, its ability to understanding other languages may require further alignments.
To this end, we create dataste 3., where beside the instruction-following task, the model can learn Chinese-English translation implicitly, and we hope this could lead to a better alignment.
> We hypothesis the succuess of [Cabrita](https://github.com/22-hours/cabrita) (i.e., the portuguese version) can be attributed to the shared subword vocabulary with English.

## Training
The code for training the Traditional-Chinese Alpaca is avaiblable [here](finetune.py).
It is based largely on [Alpaca-LoRA](https://github.com/tloen/alpaca-lora) and [Cabrita](https://github.com/22-hours/cabrita).
Our training is done on a single RTX 3090.

## Inference
The code for inferencing the trained model is avaiblable [here](inference.py).

## Next
1. Fine-tune various multi-lingual foundation models (e.g., [bloomz-7b1](https://huggingface.co/bigscience/bloomz-7b1)).
2. Construct a large-scale Traditional-Chinese instruction-following dataset. 
2. Construct domain-specific Traditional-Chinese instruction-following datasets.

*Please feel free to reach out (contact[at]nlg.csie.ntu.edu.tw) if you are interested in any forms of collaborations!*

## Reference
A large portion of our work relies on/motivated by [LLaMA](https://arxiv.org/abs/2302.13971), [Stanford Alpaca](https://github.com/tatsu-lab/stanford_alpaca), [Alpaca-LoRA](https://github.com/tloen/alpaca-lora), [ChatGPT](https://openai.com/blog/chatgpt), [Hugging Face](https://huggingface.co/), and [Cabrita](https://github.com/22-hours/cabrita).
We thanks the incredible individuals, groups, and communities for opening their amazing works!

## Citation
If you use the data or code from this repo, please cite this repo as follows
```
@misc{traditional-chinese-alpaca,
  author = {Wei-Lin Chen and Cheng-Kuang Wu and Hsin-Hsi Chen},
  title = {A Traditional Chinese Version of the Alpaca Dataset for Instruction-Finetuning},
  year = {2023},
  publisher = {GitHub},
  journal = {GitHub repository},
  howpublished = {\url{https://github.com/ntunlplab/traditional-chinese-alpaca}},
}
```
