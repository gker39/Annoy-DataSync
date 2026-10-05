# Annoy: This should be a paper Title

<p align="center">
    📑 <a href="https://huggingface.co/papers/xxxx.xxxxx" target="_blank">Paper</a> &nbsp&nbsp | &nbsp&nbsp 🌐 <a href="https://specx.github.io/" target="_blank">Project Page</a> &nbsp&nbsp | &nbsp&nbsp 🤗 <a href="https://huggingface.co/collections/sad12cxzqw/specx-67a978e28fd926b56a4f55a2" target="_blank">Released Resources</a> &nbsp&nbsp | &nbsp&nbsp 💾 <a href="https://huggingface.co/datasets/sad12cxzqw/Annoy-PyEdu-Rs" target="_blank">Dataset</a> &nbsp&nbsp | &nbsp&nbsp 📦 <a href="https://github.com/gker39/Annoy-DataSync" target="_blank">Repo</a>  
<br>

<p align="center">
    <img src="figures/overview.png" type="image/jpg"/>
<p>

## Table of contents

- [Introduction](#Introduction)
- [Released Resources](#Released-Resources)
  - [Dataset](#Dataset)
  - [Models](#Models)
- [Get Started](#Get-Started)
  - [Setup](#Setup)
  - [Data Processing](#Data-Processing)
  - [Training](#Training)
- [License](#License)
- [Citation](#Citation)
- [Acknowledgement](#Acknowledgement)

## Introduction
Annoy-DataSync is a novel approach that transforms code-based reasoning patterns into natural language formats to enhance Large Language Models' reasoning capabilities. Unlike traditional methods focusing on specific skills, our approach systematically extracts universal reasoning primitives while maintaining procedural rigor, enabling better performance across various reasoning tasks.

**Key Features & Contributions**

## Released Resources

#### Dataset

|Dataset|Link|
|-|-|
|Annoy-PythonEdu-Rs|[🤗](https://huggingface.co/datasets/sad12cxzqw/Annoy-Pyedu-Rs)|
|Annoy-PythonEdu-Rs-Raw|[🤗](https://huggingface.co/datasets/sad12cxzqw/Annoy-PyEdu-Rs-Raw)|
|LCO Benchmark|[🤗](https://huggingface.co/datasets/sad12cxzqw/LCO)|

Due to our collaborators' compliance requirements, we only release the PythonEdu-Rs subset of the Annoy(++) dataset.

### License

The released datasets **Annoy-PyEdu-Rs** and **Annoy-PyEdu-Rs-Raw** are derived from the Python-Edu subset of [SmolLM-Corpus](https://huggingface.co/datasets/HuggingFaceTB/smollm-corpus), which is released under **ODC-By**. Therefore, we release our datasets under the same **ODC-By** license.

Note: Python-Edu source code is further derived from [The Stack v2](https://huggingface.co/datasets/bigcode/the-stack-v2), which is marked as `license: other` and includes its own Terms of Use; any use of retained code snippets must also comply with those terms.

#### Models
<table>
    <tr>
        <td rowspan="2">Base Model / Training</td>
        <th colspan="2">Annoy</th>
        <th colspan="2">Annoy++</th>
    </tr>
    <tr>
        <td>Stage 1</td>
        <td>Stage 2</td>
        <td>Stage 1</td>
        <td>Stage 2</td>
    </tr>
    <tr>
        <td>Qwen 2.5 7B Coder</td>
        <td style="text-align: center; vertical-align: middle;"><a href="https://huggingface.co/sad12cxzqw/qwen2.5-7b-coder_spec_stage1">🤗</a></td>
        <td style="text-align: center; vertical-align: middle;"><a href="https://huggingface.co/sad12cxzqw/qwen2.5-7b-coder_spec_stage2">🤗</a></td>
        <td style="text-align: center; vertical-align: middle;"><a href="https://huggingface.co/sad12cxzqw/qwen2.5-7b-coder_spec_pp_stage1">🤗</a></td>
        <td style="text-align: center; vertical-align: middle;"><a href="https://huggingface.co/sad12cxzqw/qwen2.5-7b-coder_spec_pp_stage2">🤗</a></td>
    </tr>
</table>

## Get Started

### Setup

```
conda env create -f environment.yaml
conda activate annoy
```

### Data Processing

```
python ./src/build_spec_msg.py \
--input_file data/rawcode_1k.jsonl \
--output_file data/spec_1k_gens.jsonl
```

```
python ./src/batched_api_inference.py \
--input_file data/spec_1k_gens.jsonl \
--output_file data/spec_1k_gens_rev.jsonl \
--model_name "your_model_name" \
--base_url "http://localhost:8000/v1"
```

```
python ./src/check_io_pred_acc_mp_inplace.py \
--input_file data/spec_1k_gens_rev.jsonl \
--output_file data/spec_1k_gens_rev_verified.jsonl \
--python_path "python" \
--run_path "./temp/temp/temp"
```

```
python ./src/assemble_spec_demo.py \
--result_file_turn1 data/spec_1k_gens_verified.jsonl \
--result_file_turn2 data/spec_1k_gens_rev_verified.jsonl \
--output_file spec_demo_final.jsonl
```
By doing so, you can get data `data/spec_demo_final.jsonl` with the same format as in our [huggingface dataset](https://huggingface.co/datasets/sad12cxzqw/Annoy-Pyedu-Rs).

### Training
You can use any popular training framework to train your model like [llama-factory](https://github.com/hiyouga/LLaMA-Factory).

## License

The **Annoy-PyEdu-Rs** and **Annoy-PyEdu-Rs-Raw** datasets are released under **ODC-By**, the same license as the upstream SmolLM-Corpus/Python-Edu dataset.

## Citation

## Acknowledgement
We thank Koala NN, TCLV and OMEN for their valuable feedback and suggestions! 🤗🤗🤗
