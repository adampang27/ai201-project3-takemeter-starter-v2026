# Acceptance criteria


1. Overall accuracy is at least 0.80

   I want at least four out of five posts labeled correctly. Always guessing the more common label could already get around 70%, so 80% would be a useful improvement.

2. F1 for `reasoned` is at least 0.75

   These posts give the model a reason connected to a claim that it can look for. I expect it to learn that pattern, but 0.75 leaves some room for mistakes when the reasoning is worded indirectly.

3. F1 for `no_reasoning` is at least 0.70

   I expect this label to be harder because a post can sound philosophical without giving a reason for its claim. I set the target slightly lower than `reasoned` because the model has to recognize what is missing.

4. Neither label makes up more than 70% of `labels.csv`

   I expect `reasoned` to be more common in r/DeepThoughts. This keeps it from taking over the dataset and leaves at least 60 examples of each label in a 200-post dataset.

5. Accuracy on the most confident third of predictions is at least 0.90

   With about 200 posts and a 15% test split, this group will have about 10 posts. I want at least nine of those predictions to be right before I rely on the model's confident answers.
