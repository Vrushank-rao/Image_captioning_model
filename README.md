# Image_captioning_model
The captioning is done using Transformer and for diversifying the caption Transgans concept is used. 
The discriminator is a classic Deocder of the Transformer, and the generator is the combination of both Vit-encoder and decoder of the Transformer to generate the caption.
### Motivation
The main moto was to automate a process of generating a meaningful story behind an image. For many years this has been persued but the process was never perfected , my attempt isn't either, it's just a bigger step towards perfection.
## Thought process
Since the VIT architecture has proven that Transformer-Encoder can learn and extract features by making image embeddings, and as we all know that the NLP is conquered by Transformers what better option to use a Transformer-Decoder as the decoder in our architecture.
Now the image embeddings from the Vit-encoder is passed to Transformer Decoder and the caption is generated at the transformer-decoder.

# Custom Architecture 
![architecture](https://user-images.githubusercontent.com/105441109/225309814-eff98f2e-01e4-4974-8e1e-0386c99b112b.jpg)


# Training process and Evaluation

1.The model is Trained on Flicker30K dataset , the model is trained on first 20k image and tested on the last 10k images. The Training was done in 2gpus available on Kaggle.
  1. The Training is also split into 10k images and then use that to train the next 10k images , this is because there is a time limit on the notebook run time.
  2. Save the model at the end of the each epoch and then use the best model for training in the next 10k images

2.Now get the evaluation of the caption, first also check how the captioning are done by the model (in the inference files it's done)
  1. Now save all the Captions from the model vs the Ground Truth in a dictionary like this format{model_caption:list_of(ground_truth)}.
  2. The evaluation metrics from the hugging face were not working in kaggle so had to import that dictionary into colab
  3. Extract the keys as the model captions and values as a list of list.

3. Import the metrics from hugging Face in colab and evaluate the performace of the model

# Important observation
The model performed well even without getting fintuned to flicker8k dataset after being trained to flicker30k. The difference between being finetuned and not being finetuned is almost 0.001 difference in both Bleu score and Meteor score

# About Files

1."Captions_for_evaluations" file contains the dictionary where the key is the model's caption and the value is the ground truth.
  1. 'direct_flicker_8k_sentence' contains the captions where the model is not fine-tuned on flicker8k .
  2. 'flicker_8k_sentence' contains the captions where the model is fine-tuned on flicker8k .
  3. 'sentence' contains the caption after being trained in flicker30k dataset.

2.'evaluation' contains the ipyb files of the model's performance.
  1. 'evaluation_directOnFlickerModel_8k' contains the evaluations of the model pretrained on flicker30k and is directly tested on flicker8k without being finetuned.
  2. 'Evaluation_FinetunedOnFlickerModel_8k' contains the evaluations of the model pretrained on flicker30k and is tested on flicker8k after being finetuned on flicker8k.
  3. 'evaluation_of_model' conatins the evaluation of model on flicker30k images

3.'logs' contains the output of the being trained on flicker30k image dataset, there are two files because they are tarined on batches of 10k images each

4.'image-caption-custom' is the model architecture defined and also its trained on flicker30k

5.'inference' it's to see visualize the model's performance on flicker30k images dataset after being tarined on just *10k images* in that dataset

6.'inference_20k' it's to see visualize the model's performance on flicker30k images dataset after being trained on *20k images* in that dataset

7.'inference-flicker8-k' it's to see visualize the model's performance on flicker8k images dataset after being *finetuned* on train dataset of flicker8k dataset
# Few Results
![Screenshot from 2023-03-15 18-09-20](https://user-images.githubusercontent.com/105441109/225311949-a072c536-940f-46c8-b956-dc013b656095.png)
![Screenshot from 2023-03-15 18-09-49](https://user-images.githubusercontent.com/105441109/225311993-2c77a255-7c44-4649-96d2-5238b05567aa.png)





