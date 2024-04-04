# Reproduction-for-HAKE
This is MiaYuan's course project. The original code is from https://github.com/MIRALab-USTC/KGE-HAKE/tree/master. 

### These parts are done by myself (please use them with caution!):
#### 1. The model1.py is a modified model for the purpose of reproducing the results from Ablation Studies;
#### 2. figures.ipynb contains codes to reproduce all figures from the paper. Specifically, two visualization functions for modulus and phase part of relation embedding, and one visualization function for head entity embedding and tail entity embedding from any triplets.

- ## Running the code 

### Usage
```
bash runs.sh {train | valid | test} {ModE | HAKE} {wn18rr | FB15k-237 | YAGO3-10} <gpu_id> \
<save_id> <train_batch_size> <negative_sample_size> <hidden_dim> <gamma> <alpha> \
<learning_rate> <num_train_steps> <test_batch_size> [modulus_weight] [phase_weight]
```
- `{ | }`: Mutually exclusive items. Choose one from them.
- `< >`: Placeholder for which you must supply a value.
- `[ ]`: Optional items.

**Remark**: `[modulus_weight]` and `[phase_weight]` are available only for the `HAKE` model.

To reproduce the results of HAKE and ModE, run the following commands.

### HAKE
```
# WN18RR
bash runs.sh train HAKE wn18rr 0 0 512 1024 500 6.0 0.5 0.00005 80000 8 0.5 0.5

# FB15k-237
bash runs.sh train HAKE FB15k-237 0 0 1024 256 1000 9.0 1.0 0.00005 100000 16 3.5 1.0

# YAGO3-10
bash runs.sh train HAKE YAGO3-10 0 0 1024 256 500 24.0 1.0 0.0002 180000 4 1.0 0.5
```

### ModE
```
# WN18RR
bash runs.sh train ModE wn18rr 0 0 512 1024 500 6.0 0.5 0.0001 80000 8 --no_decay

# FB15k-237
bash runs.sh train ModE FB15k-237 0 0 1024 256 1000 9.0 1.0 0.0001 100000 16

# YAGO3-10
bash runs.sh train ModE YAGO3-10 0 0 1024 256 500 24.0 1.0 0.0002 80000 4
```



## Visualization
To plot entity embeddings and relation embeddings shown in the paper, run figures.ipynb after training.

## Ablation Study
To reproduce the ablation study part, replace current "models.py" file with modified model file "models1.py" through renaming the "models1.py" as "models.py". This modified python file include a modified HAKE model without the mixture bias term and HAKEm0 model which only include the phase part of the HAKE model and the ModE model that only include modulus part.

Please notice that: After adopting the modified models.py, all the results will be drawn from a setting without mixture-bias term.

To reproduce the results of HAKEm0, run the following commands.

### HAKEm0
```
# WN18RR
bash runs.sh train HAKEm0 wn18rr 0 0 512 1024 500 6.0 0.5 0.00005 80000 8

# FB15k-237
bash runs.sh train HAKEm0 FB15k-237 0 0 1024 256 1000 9.0 1.0 0.00005 100000 16 

# YAGO3-10
bash runs.sh train HAKEm0 YAGO3-10 0 0 1024 256 500 24.0 1.0 0.0002 180000 4 
```
### Training Results

The training result folder will be stored in the "models" folder, named after "{ModelName}\_{Dataset}\_{SaveID}". The results will contain a training log txt file, an entity embedding .npy file, a relation embedding .npy file, a checkpoint file and a config.json file.
All trainin results for this reproduction work can be obtained from here: https://drive.google.com/drive/folders/1--T3NalcoHRuPWlALrLfvh_PSf5PiEr1?usp=drive_link
