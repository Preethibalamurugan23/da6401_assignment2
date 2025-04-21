# Part B 
## Preethi - MM21B051

The models were trained on google colab, hence the datasets are being loaded from the drive. Please change the path to datasets in second and third cell to your dataset path. Please enter your wandb API key when prompted to log the sweeps and other details.

There are two sets of sweeps that are run in this code.
First sweep with bayesian optimization.
```sh
sweep_config = {
        'method': 'bayes',
        'metric': {'name': 'val_accuracy', 'goal': 'maximize'},
        'parameters': {
            'num_filters': {'values': [32, 64]},
            'filter_organisation': {'values': ['same', 'doubling']},
            'conv_activation': {'values': ['ReLU', 'GELU']},
            'data_augmentation': {'values': [True, False]},
            'batch_norm': {'values': [True, False]},
            'dropout': {'values': [0.0, 0.2]},
            'learning_rate': {'distribution': 'log_uniform_values', 'min': 1e-5, 'max': 1e-3},
            'epochs': {'value': 5},
            'dense_neurons': {'values': [64]},
            'dense_activation': {'values': ['ReLU', 'Tanh']},
            'weight_decay': {'distribution': 'log_uniform_values', 'min': 1e-6, 'max': 1e-2} # Add this line
        }
    }
```

Based on the results from the first sweep, a subset of parameters which gave good results were chosen for the second sweep with bayesian optimization.
```sh
sweep_config = {
    'method': 'bayes',
    'metric': {'name': 'val_accuracy', 'goal': 'maximize'},
    'parameters': {
        'num_filters': {'values': [32, 64]},
        'filter_organisation': {'values': ['same', 'doubling']},
        'conv_activation': {'values': ['GELU']},
        'data_augmentation': {'values': [True]},
        'batch_norm': {'values': [True]},
        'dropout': {'values': [0.0, 0.2]},
        'learning_rate': {'distribution': 'log_uniform_values', 'min': 1e-5, 'max': 1e-4},
        'epochs': {'value': 10},
        'dense_neurons': {'values': [64]},
        'dense_activation': {'values': ['ReLU', 'Tanh']},
        'weight_decay': {'distribution': 'log_uniform_values', 'min': 1e-3, 'max': 1e-2} # Add this line
    }
}
```
The best config found was as below, the model is tested on the test set and few predictions are visualised.

```sh
best_config = {
        'num_filters': 32,
        'filter_organisation': 'doubling',
        'conv_activation': 'GELU',
        'data_augmentation': True, 
        'batch_norm': True,
        'dropout': 0.0,
        'learning_rate': 0.0001,
        'epochs': 10,
        'batch_size': 32,
        'dense_neurons': 64,
        'dense_activation': 'Tanh',
        'weight_decay': 0.002
    }
```
