# Customized AutoML with AutoGluon, Amazon SageMaker, and AWS Lambda

This repository has been customized based on the original source code.
The customization details are as follows.

- More options to choose from in CloudFormation. (e.g. preset, evaluation metric, target variable)
- Partly modified source code suitable for deployment. This is because the model size reaches tens of gigabytes when the preset is set to    `best_quality` without any code modification. The size becomes very large because it creates a separate Out-of fold cross validation set for internally performing stacking.
- After training is completed, the results of basic evaluation indicators are additionally saved as csv files and png files such as confusion matrix, AUROC, AUPR, and feature importance
- Made very simple jupyter notebook for local inference.

## Code
* `autogluon-tab-with-test.py` is the script run by the SageMaker training job the Lambda function automatically kicks off when you upload your training data to S3. It's pre-packaged in `sourcedir.tar.gz` for the use of the pipeline. You can modify this script to reuse the pipeline with your own model training code.
* `CodeFreeAutoML.yaml` is the CloudFormation template you use to deploy the pipeline in your account.
* `lambda_function.py` is the source code for the Lambda function that kicks off the SageMaker training job when you upload your data to S3.
* `sourcedir.tar.gz` is the `autogluon-tab-with-test.py` file pre-packaged for your convenience; the pipeline requires it to be gzipped.
* `inference_on_local.ipynb` is the example code that copies the trained model from S3 and performs inference and evaluation locally.

## References
- [AWS Machine Learning blog post](https://aws.amazon.com/blogs/machine-learning/code-free-machine-learning-automl-with-autogluon-amazon-sagemaker-and-aws-lambda/).