# LLM_MoE

## About this project
In this project we will create a Mixture of Expert model using 2 different 7b models using the `mixtral` branch of [mergekit](https://github.com/arcee-ai/mergekit/tree/mixtral) and use Eleuther AI's evaluation harness and benchmark [framework](https://github.com/EleutherAI/lm-evaluation-harness/tree/main) to evaluate the LLMs that were used to create the MoE and the merged MoE model.

## License
This template is licensed under Apache 2.0 and contains the following components: 
* mergekit [GNU Lesser General Public License v3.0](https://github.com/arcee-ai/mergekit/blob/mixtral/LICENSE)
* lm-evaluation-harness [MIT License](https://github.com/EleutherAI/lm-evaluation-harness/blob/main/LICENSE.md)
* accelerate [Apache License 2.0](https://github.com/huggingface/accelerate/blob/main/LICENSE)
* bitsandbytes [MIT License](https://github.com/TimDettmers/bitsandbytes/blob/main/LICENSE)
* transformers [Apache License 2.0](https://github.com/huggingface/transformers/blob/main/LICENSE)

The assets available in this project are:

* *`merge_moe.ipynb`* - This notebook contains the commands that are needed to create a merged MoE model and run an evaluation using Eleuther AI's evaluation harness on a predefined benchmark task
* *`config.yaml`* - This is the configuration file that `mergekit` uses to create a MoE
* *`results/benchmark*.json`* - The results of the different LLMs on `asdiv` and `eq_bench`

* ## Set up instructions

This project requires the following [compute environments](https://docs.dominodatalab.com/en/latest/user_guide/f51038/environments/) to be present. Please ensure the "Automatically make compatible with Domino" checkbox is selected while creating the environment.


### Environment Requirements

**Environment Base**

***base image :*** `nvcr.io/nvidia/pytorch:23.10-py3`

***Dockerfile instructions***
```
RUN git clone https://github.com/EleutherAI/lm-evaluation-harness.git /lm-evaluation-harness && \
    cd /lm-evaluation-harness && \
    pip install -e . && \
    pip install accelerate==0.25.0 bitsandbytes==0.43.0 transformers==4.39.3

RUN  git clone -b mixtral https://github.com/arcee-ai/mergekit.git /mergekit && \
		cd /mergekit && \
 		pip install -e .
```
***Pluggable Workspace Tools*** 
```
jupyterlab:
  title: "JupyterLab"
  iconUrl: "/assets/images/workspace-logos/jupyterlab.svg"
  start: [  "/opt/domino/workspaces/jupyterlab/start" ]
  httpProxy:
    internalPath: "/{{ownerUsername}}/{{projectName}}/{{sessionPathComponent}}/{{runId}}/{{#if pathToOpen}}tree/{{pathToOpen}}{{/if}}"
    port: 8888
    rewrite: false
    requireSubdomain: false
```
Please change the value in `start` according to your Domino version.

### Hardware Requirements

