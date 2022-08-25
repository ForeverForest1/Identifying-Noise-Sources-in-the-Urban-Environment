# Capstone: Urban sound classification with UrbanSound8K dataset

# Background
Living in a dense urban environment such as Singapore means that residents are subjected to noise disturbances from various sources. For action to be taken on noise complaints, the offending noise source needs to be identified, which can be hard to isolate based on human senses alone in a dense environment. Being able to quantitatively identify the sources of noises will help speed up efforts to address noise complaints.


# Problem Statement
High-rise building residents often need to make noise complaints to the authorities (e.g. HDB and NEA). The only supporting evidence available tend to be video or sound recordings taken from the resident’s house, which can be unclear and hard to match to sources using human senses alone. Qualitative matching is also difficult to be presented as evidence to take action against the offending source. Traditional approaches to mapping sound locations make use of arrays of microphones in the vicinity of the sound source, which is something typical residents do not have access to. This project proposes training an AI model that can identify the type of urban noise based on an audio recording. The UrbanSound8K dataset will be used (https://urbansounddataset.weebly.com/urbansound8k.html). This could help provide preliminary candidates for investigating sources of noise.

# Data Dictionary

This study be using the UrbanSound8K (https://urbansounddataset.weebly.com/urbansound8k.html) dataset, which consists of 8732 labeled sound excerpts (<=4s) of urban sounds from 10 classes: air_conditioner, car_horn, children_playing, dog_bark, drilling, enginge_idling, gun_shot, jackhammer, siren, and street_music.

The metadata of each sound recording is available in a metadata csv file. The definitions of each column can be found below. For the training of our models, we will be using only the 'slice_file_name' and 'classID' columns.

slice_file_name: The name of the audio file. The name takes the following format: [fsID]-[classID]-[occurrenceID]-[sliceID].wav, where: [fsID] = the Freesound ID of the recording from which this excerpt (slice) is taken [classID] = a numeric identifier of the sound class (see description of classID below for further details) [occurrenceID] = a numeric identifier to distinguish different occurrences of the sound within the original recording [sliceID] = a numeric identifier to distinguish different slices taken from the same occurrence

fsID: The Freesound ID of the recording from which this excerpt (slice) is taken

start The start time of the slice in the original Freesound recording

end: The end time of slice in the original Freesound recording

salience: A (subjective) salience rating of the sound. 1 = foreground, 2 = background.

fold: The fold (folder) number (1-10) to which this file has been allocated.

classID: A numeric identifier of the sound class: 0 = air_conditioner 1 = car_horn 2 = children_playing 3 = dog_bark 4 = drilling 5 = engine_idling 6 = gun_shot 7 = jackhammer 8 = siren 9 = street_music

class: The class name: air_conditioner, car_horn, children_playing, dog_bark, drilling, engine_idling, gun_shot, jackhammer, siren, street_music.
 

# Model Evaluation and Results
Amongst the 3 models tested:
The best model is the CNN model with a test accuracy of 93.25%.
The next best is the RNN model, with a test accuracy of 90.27%.
The baseline model is an ANN model, with a test accuracy of 82.08%.

The CNN model was able to predict corrctly the sound classes in a few external sound clips. 


### Future work
Restricted audio file properties that can be tested - The lack of more extensive audio processing techniques in the preprocessing functions, as well as limtations in sound formats that can be read by the librosa package, means that only small wav files can be read and predicted with the model in this notebook. Future work should include more comprehensive file reading and processing methods.

Limited sound classes in the UrbanSound8K dataset - There are only 10 sound classes in the training dataset labels, which is quite small to describe the various sounds in the urban setting. E.g. weather sounds are missing. A more extensive database can be used to train the model in the future.

Dataset is not localised to Singapore context - The UrbanSound8K dataset is sourced from an open audio repository, hence the sounds might not be applicable to local context.

Need to improve ability to deal with overlapping sounds and noises - The audio clips in the UrbanSound8K dataset are relatively clear, which helps the models to easily identify the labels using MFCC features. However, in real-life, noise recordings tend to have many overlapping sources and background sounds, which is likely to significantly reduce the effectiveness of the MFCC method. More robust cleaning and preprocessing approaches such as using the mel-spectrogram should be explored.