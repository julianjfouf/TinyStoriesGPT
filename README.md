The dataset used for training: https://huggingface.co/datasets/roneneldan/TinyStories

To be completely honest I have only just noticed that there is a paper that goes along with the TinyStories dataset which I have not yet read. After a brief skim I see that this paper does what I was trying to do with this project which is to get a smaller sized GPT to be able to produce coherent and sensible stories of this simplicity.

Currently, I have trained a 43M model on about 4000 stories using a batch size of 64 and 2500 training steps. The results of this model were not too bad but they were not coherent and did not make a lot of sense. This could be for a couple of reasons. One, it may be that I did not train the model for long enough on this training dataset, leaving it with a weak understanding of how the stories are supposed to develop and how the details in the story actually connect to each other. Two, it may be that there is an issue with my tokenization or vocab size. It may be that I chose a vocab size too large, or too small. This is something that I will have to learn from either testing different vocab sizes, or it may be that this is actually something that gets covered in the paper that I am yet to read. The reason why the vocab size being too large would have a negative impact on performance is that the model would have to learn too many tokens which takes away from its focus on learning how to create coherent stories and makes it so that A) the model will have to train for longer to learn all the vocab words, B) the network may just not be large enough to understand how to use all the vocab words and converges to something that ends up being incoherent in any case. 

I expect that the issue is mostly related to the first problem I mentioned of not training for long enough. First, the training loss and testing loss were always very close to each other even until the very end of the training loop when the loss was something like 0.2 (which is already an incredibly small and acceptable training loss for me based on the networks I have trained). Second, when I trained a model of 86M parameters (expecting this to perform better), I trained it for the same number of steps as the smaller model and got it to a loss of about 0.4. I expected that this larger model would be able to produce stories of similar quality as the first (possibly even better because it is larger) but this was definitely not the case even though the difference in their losses was 0.2. This indicates that small changes in the loss of this order of magnitude are significant enough to have a large effect on the quality of the model's outputs.

I will list all of the things I wish to do for next time in a todo list at the end. Let this repo be a checkpoint in my progress of training a computationally efficient (small) model end to end on the TinyStories dataset to produce coherent stories.

As of writing this, it is the last week of the quarter and the following week is finals week so I would rather not allocate too much effort and bandwith into this effort until finals week has passed. Therefore, I will plan to achieve this goal of training a small sized GPT end to end on a large chunk of the TinyStories dataset during Spring break.

Todo:
- [ ] Read the Tiny Stories Paper
- [ ] Experiment with different methods for compiling larger training and testing datasets to improve the breadth of the content that the model can learn from (although limited by how simple and similar each of the stories are)
- [ ] Experiment with different hyperparameters for the network and tokenizer (e.g. vocab_size, total_steps, learning_rate, n_hidden, block_size, n_layers, n_heads)
