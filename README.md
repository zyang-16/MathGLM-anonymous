## GPT Can Solve Mathematical Problems Without a Calculator <br><sub>Official Pytorch Implementation</sub>

![](resources/perf.jpg)
![](resources/perf_mwp.jpg)
Previous studies have typically assumed that large language models are unable to accurately perform arithmetic operations, particularly multiplication of >8 digits, and operations involving decimals and fractions, without the use of calculator tools. This paper aims to challenge this misconception. With sufficient training data, a 2 billion-parameter language model can accurately perform multi-digit arithmetic operations with almost 100% accuracy without data leakage, significantly surpassing GPT-4 (whose multi-digit multiplication accuracy is only 4.3%). We also demonstrate that our MathGLM, finetuned from GLM-10B on a dataset with additional multi-step arithmetic operations and math problems described in text, achieves similar performance to GPT-4 on a 5,000-samples Chinese math problem
test set.



# Model Download 


## Arithmetic Tasks
For arithmetic tasks, we provide various model sizes for our MathGLM. If you wish to use our MathGLM for inference, you can download it from the following links.                                                                                                                    



## Math Word Problem
For math word problem tasks, we leverage different backbone models to tune our MathGLM on the reconstructed Ape210K dataset. Here, we provide various model sizes for our MathGLM. If you wish to use our MathGLM for inference, you can download it from the following links.                                                                                                                    


# Setup

### Environment
Our MathGLM relies on sat (SwissArmyTransformer), please ``` pip install SwissArmyTransformer ```.

Download the repo and setup the environment with:

```
conda env create -f env.yml
conda activate mathglm
```
#### Note
For arithmetic tasks and MathGLM-10B: deepspeed==0.6.0; For math word problems on MathGLM-6B: deepspeed==0.9.5



### Dataset

For arithmetic tasks, please download pre-training dataset from MathGLM-dataset-arithmetic. For math word problem, the reconstructed Ape210K dataset is provided in ```MathGLM_MWP/dataset/data.jsonl```


## Inference 

For arithmetic tashs, you can directly execute the following command to evaluate our MathGLM on the provided test dataset that contains 9,592 test cases:

```bash
cd MathGLM_Arithmetic
./inference.sh
```

For math word problem, you can evaluate our MathGLM on the Ape210K test dataset that contains 5,000 test Chinese math word problems. You can run the following  command:

```bash
cd MathGLM_MWP
./inference.sh
```


### Performance Reproduction

MathGLM achieves competitive results in comparison with the most powerful large language model GPT-4 and ChatGPT.

| Model   | ACC | RE | 
| --------- | ---------- | ---------------- | 
| GPT-4 | 18.84%    | -             |
| ChatGPT  | 10.00%    | -            | 
| MathGLM-10M  | 61.21%    | 97.83%            | 
| MathGLM-100M  | 70.28%    | 99.28%            | 
| MathGLM-500M  | 89.57%    | 99.41%            | 
| MathGLM-2B  | 93.03%    | 99.71%            | 

MathGLM-10B achieves similar performance to GPT-4 on a 5,000-samples Chinese math problem test set.
| Model   | Arithmetic_ACC | Answer_ACC | 
| --------- | ---------- | ---------------- | 
| GPT-4 | -  | 59.57%            |
| ChatGPT  | -   | 39.78%        | 
| MathGLM-Large  | 62.00%   | 50.80%            | 
| MathGLM-GLM-6B  | 64.60%   | 48.06%            | 
| MathGLM-10B  | 69.08%    | 58.68%            | 
| MathGLM-GLM2-6B  | 52.24%   | 45.48%           | 
| MathGLM-ChatGLM-6B  | 58.52%    | 42.28%           | 
| MathGLM-ChatGLM2-6B  | 50.38%    | 43.14%           | 

## Pre-training

For arithmetic tashs, run command:

```bash
cd MathGLM_Arithmetic
./pretrain.sh
```

For math word problem, run command:

```bash
cd MathGLM_MWP
./continue.sh
```
