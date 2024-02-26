# stable-diffusion-mac-tests
Trying out Stable Diffusion Locally

__Understanding Stable Diffustion__

The 3 main components of stable diffustion:

1. __U-net__: A u-net is a neural network which will estimate the noise in any given latent. To be more specific, the *input* to a u-net is a somewhat noisy latent & the corresponding *ouutput* is the estimated amount of noise in the latent representation. Now, consider that you take the input & subtract every corresponding output (i.e. the noise estimate), the expectation will be to get a more cleaner version of the latent representation itself.

2. __Variational Auto Encoder(VAE)__: The Encoder component of the autoencoder are utilized to generate the latents from the raw images. Similarly, the  decoder is utilized to re-construct the image back from the latent vector. For training the u-net, you just need the encoder. Similarly for inference, you only need the decoder component. 

3. __CLIP Text Encoder__: Consider a latent representation of the text input for which you aim to generate an image representation. The U-net will work towards estimating noise in the image, excluding the guidance aspect of the latent representation of the image.

__How do you train something like stable diffusion to work?__

Consider a model which takes a string of text tokens and encodes them into some latent space.
Similarly, consider a convolutional neural network, which will encode an immage into a latent space (of the same size as the encoding of the text).
Now, consider a joint training (or distribution) which will encode similar images & text to be 'close' to each other in the latent space. Mathematically, consider the dot product of the two embeddings to be high if the image is representative of the text & vice-versa. Similarly, dissimilar text & images will be trained to have lower dot product.

*Note: CLIP stands for Contrastive Language-Image Pre-training). The contrastive comes from the fact that during training you effectively generate a matrix of image & text embedding dot-products. The training would ideally have the diagonal as 1's and the off-diagonal elements much lower than 1, to ensure good embedding.*

