# Part B 
## Preethi - MM21B051

The models were trained on google colab, hence the datasets are being loaded from the drive. Please change the path to datasets in second and third cell to your dataset path. Please enter your wandb API key when prompted to log the model training and testing details.

The code uses a pre-trained GoogleNet model and fine tunes it.
While finetuning it, the code allows for 3 different strategies as below, which are as follows:

```sh 
fine_tuning_strategies = [
        'all',
        'classifier_only',
        'freeze_all_except_last' # New strategy
    ]
```
You can call the model then as follows
```sh
strategy='classifier_only'
    train_and_test(train_dir, test_dir, model_name, strategy, num_epochs, batch_size, learning_rate,
                           weight_decay)
```

Finally, the model is tested on the entire test set and few predictions are visualised.