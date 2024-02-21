# SRISHTI24
My Research and Submissions for the IIIT-H SRISHTI24 bearing roll-no aiml20230108] under mentor C.K. Raju Sir
# Llama 2 Fine-Tuning Guide

This guide outlines the steps to fine-tune the Llama 2 model for your specific task.

## Step 1: Install All the Required Packages

Ensure all necessary packages are installed by running the command provided in the readme.

## Step 2: Import All the Required Libraries

Import the required libraries into your Python environment as specified.
System Prompt (optional) to guide the model

User prompt (required) to give the instruction

Model Answer (required)
![image](https://github.com/Manoj010104/SRISHTI24/assets/120236387/ce5f437e-5905-46a5-9bc1-431a65ce4369)

We will reformat our instruction dataset to follow Llama 2 template.

Orignal Dataset: https://huggingface.co/datasets/timdettmers/openassistant-guanaco
Reformat Dataset following the Llama 2 template with 1k sample: https://huggingface.co/datasets/mlabonne/guanaco-llama2-1k
Complete Reformat Dataset following the Llama 2 template: https://huggingface.co/datasets/mlabonne/guanaco-llama2
To know how this dataset was created, you can check this notebook.

https://colab.research.google.com/drive/1Ad7a9zMmkxuXTOh1Z7-rNSICA4dybpM2?usp=sharing

Note: You don’t need to follow a specific prompt template if you’re using the base Llama 2 model instead of the chat version.
How to fine tune Llama 2
Free Google Colab offers a 15GB Graphics Card (Limited Resources --> Barely enough to store Llama 2–7b’s weights)
We also need to consider the overhead due to optimizer states, gradients, and forward activations
Full fine-tuning is not possible here: we need parameter-efficient fine-tuning (PEFT) techniques like LoRA or QLoRA.
To drastically reduce the VRAM usage, we must fine-tune the model in 4-bit precision, which is why we’ll use QLoRA here.


## Step 3: Reformat Your Instruction Dataset

Reformat your instruction dataset to adhere to the specified prompt template used for Llama 2 chat models.
Load a llama-2-7b-chat-hf model (chat model)
Train it on the mlabonne/guanaco-llama2-1k (1,000 samples), which will produce our fine-tuned model Llama-2-7b-chat-finetune
QLoRA will use a rank of 64 with a scaling parameter of 16. We’ll load the Llama 2 model directly in 4-bit precision using the NF4 type and train it for one epoch

## Step 4: Load Everything and Start the Fine-Tuning Process

Load your reformatted dataset and commence the fine-tuning process of the Llama 2 model.
Step 4:Load everything and start the fine-tuning process
First of all, we want to load the dataset we defined. Here, our dataset is already preprocessed but, usually, this is where you would reformat the prompt, filter out bad text, combine multiple datasets, etc.
Then, we’re configuring bitsandbytes for 4-bit quantization.
Next, we're loading the Llama 2 model in 4-bit precision on a GPU with the corresponding tokenizer.
Finally, we're loading configurations for QLoRA, regular training parameters, and passing everything to the SFTTrainer. The training can finally start!

## Step 5: Use the Text Generation Pipeline

Utilize the text generation pipeline to ask questions and generate responses from the fine-tuned Llama 2 model.
