# QA_task_using_fintuned_distilbert
A finetuned version of Bert is used for this Question-Answering task. The validation part of the 1.1 SQUAD dataset was used for the finetuning

## Introduction
I finetune a distilled version of BERT for the purposes of a Question Answering task. This model was to be finetuned using the validation part of the 1.1 version of the SQUAD dataset.
## Training
For training, the DistilBert model for Question Answering was used, along with the AdamW optimizer that was imported for the finetuning process. The SQUAD validation dataset was used, which contains 34,726 context/question/answer triplets. From those the first 33,000 were used as training data, and the last 1,726 as validation data. Details of the training procedure are described in the accompanying .ipynb files. Batch size was set to 4, because a runtime error was raised when trying to train the model with larger batches. The final train and validation losses for the 4 epochs model were 0.7206 and 2.1845, respectively. For the 10 epochs model, final train and validation losses were 0.5194 and 2.4062. The charts below depict the train and validation losses of each model.

## Validation
In a separate .ipunb file, the validation procedures of the finetuned model are shown. Using the function give_an_answer the answers of questions based on a given context were explored: Based on the sentence:
"Batman is a superhero who appears in American comic books published by DC Comics. The character was created by artist Bob Kane and writer Bill Finger, and debuted in the 27th issue of the comic book Detective Comics on March 30, 1939. In the DC Universe continuity, Batman is the alias of Bruce Wayne, a wealthy American playboy, philanthropist, and industrialist who resides in Gotham City."
the following question/answer pairs were produced:


|  | True Answer | 4 epochs model | 10 epochs model |
| :-----: | :---: | :---: | :---: |
| In which comics does Batman appear? | DC Comics | bruce wayne | DC Comics |

After this, the same function was used to go through 200 random texts from the SQUAD train set. The mean f1 score for all the answers to these texts was 0.3069 for the 4 epochs model and 0.2967 for the 10 epochs model.

## Discussion
In conclusion, it seems that the 10-epoch model did a much better job answering questions concerning Batman. In general, however, adding more epochs to the model did not seem to help produce better results. The small difference between epochs is probably due to overfitting, which appears to be happening from the 2nd epoch on for both models. In any case, given the very small amount of data the model was tuned with, it does not seem like the f1 scores were totally disappointing. It should also be noted that initial tests with a different learning rate (lr=3e-5 and lr=2e-5) did not seem to produce significantly different results either. A previous run with a batch size 8 did however have a training loss of 0.6651 and a validation loss of 2.0054 in its last, 4th epoch, which better than the respective results of the 4 epochs model discussed.
