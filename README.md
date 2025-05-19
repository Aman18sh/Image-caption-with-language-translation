Project Workflow Overview
1. Image Feature Extraction
To extract high-level visual representations, the pretrained InceptionV3 model was used as a feature extractor. Each image from the Flickr8k dataset (which contains 8,091 images with five captions each) was resized and preprocessed before being passed through InceptionV3. The output of the final pooling layer was captured, resulting in a 2048-dimensional dense feature vector representing the image content.

2. Caption Generation
A custom encoder-decoder model was built for generating captions. The encoder processes the image features while the decoder, an LSTM network, predicts the sequence of words to describe the image. The decoder was trained to predict the next word in the sequence given the image features and the previously generated words. The input to the model was (image_features, input_seq) and the output was the next_word in the caption. A greedy decoding strategy was implemented during inference for caption generation, where the model selects the word with the highest probability at each step. (Support for Beam Search was also considered for better caption diversity.)

3. Caption Translation
To enhance accessibility and multilingual support, the generated English captions were translated into other languages such as French and Hindi using the googletrans library. This enabled the system to serve diverse linguistic audiences by providing captions in their native language.

4. Audio Generation
To provide a multimodal user experience, the translated captions were converted to speech using Google Text-to-Speech (gTTS). The resulting audio files were saved and played within Jupyter Notebook using IPython.display.Audio, enabling users to hear the captioned description of the image in their chosen language.
