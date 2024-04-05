# LLM_MoE

## About this project

## License
This template is licensed under Apache 2.0 and contains the following components: 

The assets available in this project are:

* *`merge_moe.ipynb`* -
* *`config.yaml`* -
* *`results/benchmark\*.json`* -

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

