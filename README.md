# text-nano

Learning to make an LLM from scratch in C.

https://www.youtube.com/watch?v=kCc8FmEb1nY

https://huggingface.co/papers/2509.14008

https://github.com/ArturoNereu/AI-Study-Group, https://www.youtube.com/watch?v=wjZofJX0v4M 

[OpenCL tutorials](https://www.reddit.com/r/gpgpu/comments/wsaosn/comment/iljzu2m/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button)

Transformer takes in a string of tokens (corresponding to a piece of text), pass them through a function. and outputs weights for what the next token could be. Appending one of the most highly weighted, then repeating the process, allows you to generate (somewhat) sensible text. The internal function is as follows:

- **Tokenization:** the model has a predefined **vocabulary** of tokens, which the input text is tokenized into (by some handmade algorithm)
- **Embedding:** each token is associated with a high-dimensional vector (determined by training an "embedding matrix" wherein each column corresponds to the vector of a token, beginning random but learning through data) that somehow "encodes the meaning" of the token to the transformer. tokens with similar meanings tend to have nearby vectors.
- **Transformation:**
  - the list of vectors undergo an operation within an "attention block," wherein tokens are able to exchange information with eachother (an attention block has a fixed "context size," for GPT-3 it was 2048 tokens) (note the difference between "fashion model" and "AI model" can only be distinguished through surrounding context; note that a king that was tyrannical has a much different semantic feel than one who was benevolent)
  - they then undergo an operation within a "feed forward layer," wherein tokens independently update themselves based on some function
  - these two previous processes repeat many times
- **Unembedding:** at the end, the hope is that every vector in the list has a "meaning" that will predict the token following it. to do this, we multiply a vector (for the purpose of the output, the final vector) with an **unembedding matrix** (that starts random but learns through training) that maps this vector to a list of values, one for each possible token, then use the softmax algorithm (that also can take in a temperature) to produce the output probability distribution over all possible tokens

a tensor is a higher-dimensional array
