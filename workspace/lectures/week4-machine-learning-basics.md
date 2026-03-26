# Week 4 Lecture Notes: Machine Learning Fundamentals

## What is Machine Learning?

### Definition
Machine Learning is the study of algorithms that can learn from and make predictions on data.

### Types of Learning
- **Supervised Learning**: Learn from labeled examples
- **Unsupervised Learning**: Find patterns in unlabeled data
- **Reinforcement Learning**: Learn through interaction and rewards
- **Semi-supervised Learning**: Mix of labeled and unlabeled data

### Why Machine Learning?
- **Pattern recognition**: Find complex patterns in data
- **Prediction**: Make informed guesses about future events
- **Automation**: Reduce manual effort in decision making
- **Scalability**: Handle large amounts of data

## Supervised Learning

### Problem Setup
- **Training data**: Pairs of inputs and correct outputs
- **Learning algorithm**: Creates model from training data
- **Prediction**: Apply model to new inputs

### Example: Email Classification
- **Input**: Email text
- **Output**: Spam or not spam
- **Training**: Learn from labeled emails
- **Prediction**: Classify new emails

### Key Concepts
- **Features**: Measurable properties of inputs
- **Labels**: Correct outputs for training
- **Model**: Mathematical representation of patterns
- **Generalization**: Performance on new, unseen data

## Training and Testing

### Data Splitting
- **Training set**: Used to train the model (60-80%)
- **Validation set**: Tune model parameters (10-20%)
- **Test set**: Final evaluation (10-20%)

### Overfitting
- **Definition**: Model fits training data too closely
- **Symptoms**: Perfect training accuracy, poor test accuracy
- **Prevention**: Cross-validation, regularization, simpler models

### Underfitting
- **Definition**: Model too simple to capture patterns
- **Symptoms**: Poor performance on both training and test data
- **Prevention**: More complex models, better features

## Common Algorithms

### Decision Trees
- **How it works**: Series of if-then rules
- **Advantages**: Interpretable, handles mixed data
- **Example**: If age < 30 and income > 50K then approve loan

### Neural Networks
- **How it works**: Layers of interconnected nodes
- **Advantages**: Can learn complex patterns
- **Training**: Adjust connection weights using backpropagation

### Support Vector Machines
- **How it works**: Find optimal boundary between classes
- **Advantages**: Effective in high dimensions
- **Kernel trick**: Handle non-linear boundaries

## Model Evaluation

### Classification Metrics
- **Accuracy**: (Correct predictions) / (Total predictions)
- **Precision**: (True positives) / (True positives + False positives)
- **Recall**: (True positives) / (True positives + False negatives)
- **F1-score**: Harmonic mean of precision and recall

### Regression Metrics
- **Mean Squared Error (MSE)**: Average of squared differences
- **Mean Absolute Error (MAE)**: Average of absolute differences
- **R-squared**: Proportion of variance explained

### Cross-Validation
- **k-fold CV**: Split data into k parts, train on k-1, test on 1
- **Repeated CV**: Run multiple times for stability
- **Stratified CV**: Maintain class proportions

## Feature Engineering

### What are Features?
- **Raw features**: Direct measurements
- **Derived features**: Computed from raw features
- **Categorical features**: Convert to numerical (one-hot encoding)
- **Text features**: Bag of words, TF-IDF, embeddings

### Feature Selection
- **Filter methods**: Statistical tests (correlation, chi-square)
- **Wrapper methods**: Use model performance to select features
- **Embedded methods**: Feature selection during model training

### Dimensionality Reduction
- **Principal Component Analysis (PCA)**: Linear projection to lower dimensions
- **t-SNE**: Non-linear projection for visualization
- **Autoencoders**: Neural network approach to compression

## Bias and Fairness

### Types of Bias
- **Sampling bias**: Training data doesn't represent population
- **Label bias**: Incorrect or inconsistent labels
- **Algorithmic bias**: Model amplifies existing biases

### Fairness Metrics
- **Demographic parity**: Equal outcomes across groups
- **Equal opportunity**: Equal true positive rates
- **Predictive equality**: Equal false positive rates

### Mitigation Strategies
- **Pre-processing**: Modify training data
- **In-processing**: Constrain model during training
- **Post-processing**: Adjust predictions after training

## Practical Considerations

### Data Quality
- **Garbage in, garbage out**: Poor data leads to poor models
- **Data cleaning**: Handle missing values, outliers
- **Data augmentation**: Generate additional training examples

### Computational Resources
- **Training time**: Some models require significant computation
- **Memory usage**: Large datasets need appropriate hardware
- **Scalability**: How well does the approach work at scale?

### Deployment Challenges
- **Model drift**: Performance degrades over time
- **Monitoring**: Track model performance in production
- **Updates**: When and how to retrain models

## Discussion Questions

1. What are the differences between supervised and unsupervised learning?
2. How do you know if your model is overfitting?
3. What are the trade-offs between different machine learning algorithms?
4. How can we ensure machine learning systems are fair and unbiased?

## Key Takeaways

- Machine learning enables computers to learn from data
- Training and testing are essential for reliable models
- Overfitting is a common pitfall that must be avoided
- Feature engineering is often more important than algorithm choice
- Fairness and bias are critical considerations in ML systems
- Real-world deployment requires ongoing monitoring and maintenance

## Future of Machine Learning

- **Deep learning**: Neural networks with many layers
- **Transfer learning**: Apply knowledge from one domain to another
- **Automated ML**: Tools that automate model selection and tuning
- **Explainable AI**: Making ML models more interpretable
- **Federated learning**: Train models across distributed devices