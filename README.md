# Reigen Arataka AI Chat Bot

An AI discord bot that can simulate a conversation with the greatest psychic of the 21st century, Reigen Arataka from [Mob Psycho 100](https://en.wikipedia.org/wiki/Mob_Psycho_100)!

Credits to Lynn Zheng and her [Discord AI Chatbot tutorial](https://www.freecodecamp.org/news/discord-ai-chatbot/) for helping me build this.

The chatbot uses the [Microsoft DialoGPT conversational model](https://huggingface.co/microsoft/DialoGPT-medium) that has been trained with [transcripts of season 1, 2, and the OVA from this Kaggle dataset](https://www.kaggle.com/datasets/faebots/mp100-episodes). The dataset has almost 1000 lines from Reigen and I trained it for 12 epochs to give a perplexity of 1.6988. The perplexity represents how confused the model is so the higher the perplexity, the more confused the model is. With this amount of data, the model took around 40 minutes to train.

## Problems I Encountered
I had trouble reading the CSV file in Python as it wasn't properly formatted so I used the txt file to parse the script into a CSV file that would work. I encountered the error `'utf-8' codec can't decode byte 0xff in position 0: invalid start byte` but I managed to solve it through [this Kaggle post](https://www.kaggle.com/code/paultimothymooney/how-to-resolve-a-unicodedecodeerror-for-a-csv-file).

Even though Reigen only has almost 1000 lines, he talks a lot per line which is too much for my GPU to handle so I run out of memory. That's why I decreased `self.per_gpu_train_batch_size` from 4 to 3 in order to train the model.

1.6988 is a very low perplexity but I'm guessing that I have trained the model for too many epochs, given it's small number of lines. The model is so in character that it mainly repeats direct lines from the transcript. It also sometimes says lines from other characters.

If you want to try out my chatbot, you can go [here](https://huggingface.co/sophiadt/DialoGPT-medium-reigen?text=Hi+Reigen%21) where it's hosted on Hugging Face's Model Hub.

## Project Files

* `model_train_upload_workflow.ipynb`: Notebook to be run in Google Colab to train and upload the model to Hugging Face's Model Hub
* `mp100.txt`: The text file I used to gather the data from
* `parse_script.ipynb`: Notebook to be run in Google Colab in order to turn the text file script into a workable CSV file
* `main.py`: Script to be imported into a Repl.it Python Discord.py project
* `stay_alive.py`: Script to keep the discord bot alive for half an hour after main.py is run

## Resource Links
* [Lynn Zheng's tutorial on freeCodeCamp](https://www.freecodecamp.org/news/discord-ai-chatbot/)
* [Lynn Zheng's video tutorial on YouTube](https://youtu.be/UBwvFuTC1ZE)
* [Mob Psycho 100 transcript dataset on Kaggle](https://www.kaggle.com/datasets/faebots/mp100-episodes)
* [My Hugging Face Model](https://huggingface.co/sophiadt/DialoGPT-medium-reigen)
