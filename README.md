# English-Spanish Sequence-to-Sequence Translator with Attention (Keras/TensorFlow)

This project implements a basic sequence-to-sequence (seq2seq) model with an attention mechanism for English-to-Spanish translation, built using Keras and TensorFlow. The primary goal of this notebook is to demonstrate the fundamental concepts and architecture of an encoder-decoder model with attention, rather than achieving production-level translation quality.

## Project Overview

This notebook serves as an educational exercise to understand the inner workings of a neural machine translation system. It showcases:

*   **Encoder-Decoder Architecture:** A standard seq2seq setup where an encoder processes the input sequence and a decoder generates the output sequence.
*   **Attention Mechanism:** An added Self-Attention layer that allows the decoder to focus on different parts of the input sequence during the translation process, improving the contextual understanding.
*   **Keras/TensorFlow Implementation:** Demonstrates how to build and train such a model using the high-level Keras API within the TensorFlow framework.

## Architecture Details

The model consists of:

1.  **Encoder:**
    *   An `Embedding` layer to convert input tokens into dense vector representations.
    *   A `LSTM` layer that processes the embedded input sequence and outputs a context vector (states) and a sequence of hidden states.
    *   `Dropout` for regularization.

2.  **Decoder:**
    *   An `Embedding` layer for target sequence tokens.
    *   A `LSTM` layer initialized with the encoder's final states.
    *   A custom `SelfAttention` layer that calculates attention weights between the decoder's current state and the encoder's output sequence.
    *   `Dropout` for regularization.
    *   A `Concatenate` layer to combine the decoder's output with the attention output.
    *   A `Dense` layer with `softmax` activation to predict the next token in the output vocabulary.

## Data

The model is trained on a small, synthetic parallel corpus of English and Spanish sentences (currently 15 samples). Due to the very limited dataset size, the model's translation performance is basic and primarily serves to illustrate the architecture rather than practical translation capabilities.

## Key Features Implemented

*   **Custom `SelfAttention` Layer:** A custom Keras layer for implementing the attention mechanism.
*   **Data Preprocessing:** Tokenization, sequence padding, and one-hot encoding of target sequences.
*   **Regularization:** `Dropout` layers and `L2` regularization applied to LSTM and Dense layers to combat overfitting.
*   **Early Stopping:** Utilized `EarlyStopping` callback to monitor validation loss and prevent prolonged training on overfit models.
*   **Inference Model:** Separate encoder and decoder inference models are constructed for sequence generation at test time, where the decoder generates one token at a time.

## Observations

With the current small dataset, the model exhibits significant overfitting and struggles to generalize. The inference results show repetitive outputs (`'es es es'`), indicating that the model defaults to frequently observed tokens due to insufficient data for learning complex linguistic patterns. To achieve a functional translation model, a substantially larger and more diverse dataset would be required.

## Setup and Usage

1.  **Dependencies:** Ensure you have TensorFlow, Keras, and NumPy installed.
2.  **Run the Notebook:** Execute the cells sequentially. The notebook includes sections for:
    *   Setting up the environment.
    *   Defining sample data.
    *   Data preprocessing (tokenization, padding).
    *   Defining the `SelfAttention` custom layer.
    *   Building and compiling the seq2seq model with attention.
    *   Training the model.
    *   Plotting training history.
    *   Setting up and testing inference models.

To observe better translation quality, expand the `input_texts` and `output_texts` lists with many more diverse English-Spanish sentence pairs.
