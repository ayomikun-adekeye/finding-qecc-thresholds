# finding-qecc-thresholds
In the notebooks in this repo, I estimated the _thresholds_ of 4 types the _surface code_ using _Monte Carlo_ sampling.

A threshold in this context, is the physical error rate where increasing the code distance of a particular quantum error correction code, increasingly supresses the logical error rate. 

Monte Carlo sampling is just a computational method that can be summed up like this: more trials => higher guess accuracies. Rather than finding the threshold with some formula, for each quantum error correction code, I picked 5 code distances and plotted the logical error rate against the physical error rate. For typical simulations like this, plotting the results usually reveals a point where all the lines seem to clearly cross, or where there's an increasing supression of the logical error rate. That's the threshold. Above that threshold, increasing higher code distances are useless, or even boost logical errors.
