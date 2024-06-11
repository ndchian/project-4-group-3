# Identification of various mushroom species as edible, definitely poisonous, or of unknown edibility(classified as poisonous)

## Project 4 (Group: 3) - University of Minnesota- Data Visualization and Analytics Bootcamp

### Collaborators:
* [Ashley Anderson](https://github.com/AshleyKAnderson) <br>
* [Kolton Ascheman](https://github.com/K01t0N) <br>
* [Nora Chian](https://github.com/ndchian)<br>
* [Atul Shiwakoti](https://github.com/atulshi)<br>

## Project Overview:
Determination of various mushroom species as edible or not (also, classified as poisonous). To support this binary task, the largest and most comprehensive attribute-based data available is collected. Thanks to natural language processing, the primary data are based on a textbook for mushroom identification and contain 173 species from 23 families. All the sources for data are mentioned in given section below.
    
### Dataset: 
[Secondary Mushroom](https://archive.ics.uci.edu/dataset/848/secondary+mushroom+dataset)

The dataset is in the .csv format and contains more than 22,000 rows and 21 columns. It includes 61069 hypothetical mushrooms with caps based on 173 species (i.e. 353 mushrooms per species). Each mushroom is identified as definitely edible, definitely poisonous, or of unknown edibility and not recommended (the latter class was combined with the poisonous class).

### Sources and References
   1)  Dataset: [Secondary Mushroom](https://archive.ics.uci.edu/dataset/848/secondary+mushroom+dataset)
   2)  Introductory Paper: [Creation and simulation of dataset](https://www.semanticscholar.org/paper/Mushroom-data-creation%2C-curation%2C-and-simulation-to-Wagner-Heider/336be248b6f1c5d77c3c93e89f2e19e7344b0250)
   3)  [Google Developer Machine Learning Guide](https://developers.google.com/machine-learning/decision-forests/practice)
   4)  [YDF Documentation](https://ydf.readthedocs.io/en/stable/)

## Data Preprocessing

### Deciding on columns with missing values
Five columns contained a significant amount of missing values (more than 60% of the values for that column). Our group ultimately decided to drop those columns entirely. We figured that those columns would not contribute much to the models anyway, since there is so little data.

### Separating, scaling, and preprocessing data for models

For both the random forest classifier and logistic regression models, X is assigned from dropping the target variable (class) from the rest of the data. It is then split between categorical and numeric columns. `StandardScalar` scales the numerical data, so that equal importance is placed on the features. `pd.get_dummies` is used on the categorical variables to convert them into a format that the algorithm will understand. The two parts were then concatenated back into a single `X_clean` variable.

For the gradient boosted trees model, the 'class' column was set as the label and the cleaned data set was split 30/70 into the testing and training datasets respectively. 

### Creating a PCA version of the data

Because the dataset contains more than 80 columns after preprocessing, a second dataset was created. PCA was used on this dataset using `fit_transform`, reducing the number of dimensions for the model to train on. The `n_components` were set to 5 to allow for the highest accuracy without having more dimensions than needed.

## Results and Analysis

### Optimization

For both the logistic regression model and the random forest classifier, the PCA data was used in a second iteration for each model type. This increased the accuracy readings for both models at least 16%.

For the gradient boosted tree model, our initial model had already achieved 100% accuracy, but we wanted to provide a way to be able to optimize this model if we needed it. In the initial model, the `num_trees` had 100 trees as the input and one way to optimize the model is to increase this number. In the example we provided in the notebook, this was increased to 1,000 trees which also achieved 100% accuracy.

### Final Results

The random forest model trained on PCA data dramatically outperformed the logistic regression model with either the original dataset or PCA as well as the random forest model with original data. In a use case like this that is safety-related, it is crucial to obtain a near-perfect accuracy. Likewise, another major component is eliminating as many false negatives as possible. The precision and recall values for both outcomes are 98-99%.

The YDF gradient boosted trees model did come in with 100% accuracy in identifying the edible and poisonous mushrooms. However, this model type does have a drawback of being more likely to overfit the data. For the best quality results, both the gradient boosted tree and random forest results should be taken into account.

The logistic regression model with pca data, while maintaining a recall for poisonous outcomes at 79%, still struggles to keep an overall accuracy of 72%, compared to the random forest model's 99%. This indicates that the pca is complex enough that it requires an algorithm more nuanced than a simple regression.

The worst performing models were the ones trained on the regular, unoptimized dataset. Trained on this data, the random forest and logistic regression algorithms had accuracy scores of 52% and 56%, respectively. Based on these performance metrics, data optimization was a huge help in achieving the desired results.

The confusion matrices and accuracy results can be found in either our slide deck or in the 'Results' folder of this repository as can the YDF gradient boosted model tree. If you are running our notebook, best results will be achieved in using Google Colab. 

## Presentation Tools

Please view our [slide deck](https://docs.google.com/presentation/d/1fP5_myl5a4beyzoj1ECBHwvMkO1uI4Y_84e1jNgDBOE/edit?usp=sharing) here. 
