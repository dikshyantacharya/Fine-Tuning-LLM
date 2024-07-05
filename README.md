# Fine-Tuning-LLM

## Project Overview

This project implements fine-tuning of the Llama3 model for information extraction from text documents. The model is automatically quantized using Unsloath AI and then fine-tuned with custom datasets. The primary goal is to extract structured information from unstructured text and output it in JSON format.

## Features

- Automatic download and quantization of the Llama3 model
- Training and validation dataset upload functionality
- Fine-tuning of Llama3 for information extraction 
- Analysis of Training of Model
- Upload a PDF file and receive extracted information in JSON format from finetuned Model

## Dataset Requirements

The training and validation datasets must be JSON files with the following names and structure:

- Training dataset: `extract_information_train.json`
- Validation dataset: `extract_information_val.json`

Each JSON file should contain an array of JSON objects, where each object is formatted as follows:

```json
{
    "training_text": "<SYSTEM_PROMPT>.....\n<USER_PROMPT>.....\n<TEXT: *** ... ***>\n<ASSISTANT: The extracted information required in JSON format is:\n<extracted_information_in_json> ..... </extracted_information_in_json>",
    "validation_text": "<SYSTEM_PROMPT>\n<USER_PROMPT>\n<TEXT: *** ... ***>\n<ASSISTANT: The extracted information required in JSON format is:\n<extracted_information_in_json>"
}
```

The System Prompt and User Prompt must be adjusted as per the required specific task. For my case, I had the dataset in the following format:
Specific Task Dataset Format

```json

{
    "training_text": "\nSYSTEM_PROMPT: \nYou are an ASSISTANT who is expert in Information Extraction from a text and putting it in JSON Format in text summarization. Given a text between <original_text> and </original_text>, your task is to accurately extract the specified information without errors between <extracted_information_in_json> and </extracted_information_in_json>. If a specific piece of information is not available, write '-' as values for its key. Do not include any keys that are not listed. For arrays, provide key-value pairs for each element in the array as dictionaries.\n\nUSER_PROMPT: \nFrom the provided text, extract the following information in JSON format as key-value pairs. The keys are:\n- isin\n- emittent_name\n- produkt_name\n- laufzeit_start/Erstellungsdatum\n- bewertungstag\n- zahltag\n- waehrung\n- nominal\n- Basiswert/Underlying\n- Arrays of dictionaries with keys: Datum, Strike (in%)\n\nThe text is delimited by three asterisks (***). Provide the extracted information in JSON format.\n\nTEXT: ***\nAll_Text_Of_PDF\n***\n\nASSISTANT: The extracted information required in JSON format is: \n<extracted_information_in_json>\nAnswer_In_Json_Format\n</extracted_information_in_json>",
    
    "validation_text": "\nYou are an ASSISTANT who is expert in Information Extraction from a text and putting it in JSON Format in text summarization. Given a text between <original_text> and </original_text>, your task is to accurately extract the specified information without errors between <extracted_information_in_json> and </extracted_information_in_json>. If a specific piece of information is not available, write '-' as values for its key. Do not include any keys that are not listed. For arrays, provide key-value pairs for each element in the array as dictionaries.\n\nUSER_PROMPT: \nFrom the provided text, extract the following information in JSON format as key-value pairs. The keys are:\n- isin\n- emittent_name\n- produkt_name\n- laufzeit_start/Erstellungsdatum\n- bewertungstag\n- zahltag\n- waehrung\n- nominal\n- Basiswert/Underlying\n- Arrays of dictionaries with keys: Datum, Strike (in%)\n\nThe text is delimited by three asterisks (***). Provide the extracted information in JSON format.\n\nTEXT: ***\nAll_Text_Of_PDF\n***\n\nASSISTANT: The extracted information required in JSON format is: \n<extracted_information_in_json>\n"
}
```
## Running The Script
- Upload Training and Validation Datasets
- You will be prompted to upload extract_information_train.json and extract_information_val.json during the script execution.

## Start Training

The script will fine-tune the model using the uploaded datasets. The training dataset is used to train the model, and the validation dataset is used to evaluate the model's performance. The hyperparameter tuning can be done by changing the model's parameters.

## Upload a PDF for Extraction

Once the training is complete, you will be prompted to upload a PDF file for information extraction. The model will process the PDF and provide the extracted information in JSON format.
Notes

   - The datasets must already contain the required input with prompt engineering and output for training text.
   - Only 20 training data entries were required to achieve accurate results in this implementation.
   - The model was trained on Google Colab with a minimum requirement of 16GB of GPU. If the text in datasets is too long, then more GPU will be required. Training on Kaggle using UnslothAI encountered problems during the training of the model.
   - The script was written with the help of script: https://colab.research.google.com/drive/135ced7oHytdxu3N2DNe1Z0kqjyYIkDXp?usp=sharing

## Author Information

**Name:** [Dikshyant Acharya]

**Email:** [dikshyantacharya@google.com]
