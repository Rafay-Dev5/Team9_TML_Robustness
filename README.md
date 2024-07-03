# TML_Team9_Robustness

The jupyter notebook provides the code for Adversarial Robustness. Firstly, we have divided the data into training and validation sets. All the images are converted into Tensors, and Dataset and Dataloader objects are prepared.

Then, a pretrained ResNet34 model is picked before PGD and FGSM attacks are defined. ResNet34 is picked to ensure that the model is neither too weak nor too complex. 

In PGD, we have defined a very small perturbation budget (epsilon) and step size is approximately equal to epsilon/iterations. During each iteration, the image is moved closer to the decision boundary by adding a delta to it. It is ensured that the delta remains in the perturbation budget. I did try random starts for the delta, but the results were poorer than zero initialised starts.

For FGSM, there is one single step in the similar fashion as PGD. There are no iterations.

The ResNet model is adversarially trained using PGD with early stopping to ensure that there is no overfitting. Standard training is used because Free and Fast reduce robustness slightly even though they are faster adversarial training procedures. The optimizer is SGD with momentum and the loss function being used is the CrossEntropyLoss.

Finally, the model is evaluated for its clean accuracy, robustness (fgsm), and robustness (pgd) accuracy

The best performing model had a clean accuracy of around 52% with robustness for both attacks hovering around 35%. 