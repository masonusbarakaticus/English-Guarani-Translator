# English-Guarani-Translators
Low-Resource Data-Driven Transformer Analyses

# Necessary Files
To run and successfully train all the models, you need to download "NLLB.en-gn.gn", "NLLB.en-gn.en", "grn_Latn.devtest", and "eng_Latn.devtest" from https://drive.google.com/drive/folders/1sZ76dshqF9CHAGL6L6k_0KrxYkqBI2k3?usp=sharing and place them in the same directory as whatever model you are running.
For NLLB, download the following with en-gn.tmx, eng_Latn.devtest, and grn_Latn.devtest: https://drive.google.com/drive/folders/1gPn3k6jrFnx-ZUg34AnIBSCeL9lD3w5m?usp=drive_link

# ByT5 (Mason Barakat)
The ByT5 model is a byte-based model that looks at each character in a given string and converts it to its ASCII value. This makes the model robust and relieves you of any typical worries associated with language-specific preprocessing tasks, like normalization and splitting on special characters. The model simply takes them as they come. However, it is more difficult for the model to reliably pick up on language-specific patterns than subword-based models. This is demonstrated in the model's low Chrf++ score, though the score is expected after only training on 10,000 sentence pairs. It indicates that the model is well suited for translation tasks, but might not be your first pick if it is a lower-resource language. For higher-resource languages, you can take advantage of its language-agnostic tokenizer for language translation tasks that are from one script to another (Arabic-Chinese, for example). If you run the model in a colab environment, be sure to uncomment the relevant file-path code. Requires: pip install of protobuf and sentpiece, 
transformers: 3.5.1, 
evaluate: 0.4.3, 
datasets: 3.5.1

# BERT→GPT-2 (Ben Horlbeck)
This model has a unique strategy where we used the Bert encoder and the gpt-2 as a decoder using the hugging face tools we have. More specifically we used the Encoder Decoder Model. Both of the components are pretreated on the more general aspects of text. That being said, the translation task English to Guarani was trained from scratch out of the 10,000 sentence pairings we used in the project. This ended with us creating a special tokenizer that was using Berts input as the rule and then we then kind force the gpt 2 token to act the same way. The model overall performed poorly which was expected and had a Chrf++ score of 11.38. This is good however for the experimental nature of these models and it was really to see what we could do with a low resource translation without task knowledge from the past.

# NLLB (Ray Scherer)
No language left behind (NLLB) is a language model designed by Meta specifically for translating low resource languages. It was pretrained on the NLLB dataset as well as the FLORES-200 dataset, which is likely the cause of its elevated ChrF++ score. The expected metric should be around 38.16, but small variations are possible. To run the widget translator, simply run the translator block after a model has been trained. For this model specifically, run in an environment where it is possible to mount a google drive so that file paths are not affected, or adjust the filepaths to wherever the CompLing folder is placed. The widget should be mostly functional but will occasionally run into some problems. Including punctuation often helps.   
Requires the following packages:  
transformers: 4.51.3  
datasets: 3.5.1  
evaluate: 0.4.3  
accelerate: 1.6.0  
sacrebleu: 2.5.1  
All hyperparameters are predefined and should not be changed to ensure similar results.

This was run on google colab using a T4 GPU, so ideally a similar or identical environment should be used to replicate results. This also allows for mounting the datafiles from google drive which is used in the code.

# gtranslate (Ray Scherer)
This was used specifically to get a reference ChrF++ score for google translate, which uses google neural machine translation. The output should be around 32.24. The setup for this should be identical to the NLLB script (set up in colab and mount drive).   
Requires the following packages:   
datasets: 3.5.1  
deep-translator: 1.11.4   
sacrebleu: 2.5.1  

# mBART-50 (Jake Burton)
multilingual BART-50 is the latest version of Facebook's mBART, which is built to include even more languages and hidden layers. It is pretrained on a large multilingual corpus, and each language has its own tag in the form of <en_XX> (english). Because it wasn't trained on single direction language to language translation it is fluid to translate one language to another without needing to be specifically trained on that scenario. This was edited to include the Guarani language, using the tag <gn_XX>. It is fine tuned on this language using the NLLB gn and en corpus. The accuracy is tested via ChrF++ once the model is complete. mBART uses built in translation functions. Areas have been included in the file to test out this translation function and ensure the model was successful. 
Requires the following packages:  
transformers[sentencepiece]: 4.51.3  
datasets: 3.5.1  
evaluate: 0.4.3  

