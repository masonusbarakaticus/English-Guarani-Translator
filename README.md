# English-Guarani-Translator
Low-Resource Data-Driven Transformer Analyses

# Neccesary Files for bert-gpt
In order to run the file within bert-gpt folder you must download the folder located at "https://drive.google.com/drive/folders/1sZ76dshqF9CHAGL6L6k_0KrxYkqBI2k3?usp=sharing" and place it in the bert-gpt folder

# Necessary Files for NLLB_2
To run the file, you will need to download the folder datafiles at the drive: 

# Necessary Files
To run and successfully train all the models, you need to download "NLLB.en-gn.gn", "NLLB.en-gn.en", "grn_Latn.devtest", and "eng_Latn.devtest" from "https://drive.google.com/drive/folders/1sZ76dshqF9CHAGL6L6k_0KrxYkqBI2k3?usp=sharing" and place them in the same directory as whatever model you are running.

# ByT5
The ByT5 model is a byte-based model that looks at each character in a given string and converts it to its ASCII value. This makes the model robust and relieves you of any typical worries associated with language-specific preprocessing tasks, like normalization and splitting on special characters. The model simply takes them as they come. However, this makes it more difficult for the model to reliably pick up on language-specific patterns that subword-based models might have an easier time with. This is demonstrated in the model's lower Chrf++ score, though the score is expected after only training on 10,000 sentence pairs. It indicates that the model is well suited for translation tasks, but might not be your first pick if it is a lower-resource language. For higher-resource languages, you can take advantage of its language-agnostic tokenizer for language translation tasks that are from one script to another (Arabic-Chinese, for example). If you run the model in a colab environment, be sure to uncomment the relevant file path code.
