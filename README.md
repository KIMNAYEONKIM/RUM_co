# RUM
This is a PyThon implementation of RUM. 

# Original model training
```
python main_train.py --dataset {dataset name} --arch {model architecture} --epochs {epochs} --lr {learning_rate} --batch_size {batch_size}
```

# Unlearning

For each algorithm, we use --mem parameter for memorization experiments and --group_index for ES experiments.

## RUM

```
python main_rum.py --unlearn ${unlearn method} --mem mix --num_indexes_to_replace 3000 --dataset {dataset name} --arch {model architecture} --epochs {epochs for training the original model} --lr 0.1 --batch_size 256
```


### Retrain

```
python main_forget.py --unlearn retrain --num_indexes_to_replace 3000 --unlearn_epochs 30 --unlearn_lr 0.1 --mem {memorization group} --group_index {ES group} 
```

### Fine-tune

```
python main_forget.py --unlearn FT --num_indexes_to_replace 3000 --unlearn_lr 0.01 --unlearn_epochs 10 --mem {memorization group} --group_index {ES group} 
```

### l1-sparse

```
python main_forget.py --unlearn FT_prune --num_indexes_to_replace 3000 --alpha ${alpha} --unlearn_lr 0.01 --unlearn_epochs 10 --mem {memorization group} --group_index {ES group} 
```

### NegGrad

```
python main_forget.py --unlearn GA --num_indexes_to_replace 3000 --unlearn_lr 0.0001 --unlearn_epochs 5 --mem {memorization group} --group_index {ES group} 
```

### NegGrad+

```
python main_forget.py --unlearn NG --num_indexes_to_replace 3000 --alpha ${alpha} --unlearn_lr 0.01 --unlearn_epochs 5 --mem {memorization group} --group_index {ES group} 
```

### SCRUB

```
python main_forget.py --unlearn SCRUB --num_indexes_to_replace 3000 --msteps 4 --kd_T 4.0 --beta ${beta} --gamma ${gamma} --unlearn_lr 5e-3 --unlearn_epochs 5 --mem {memorization group} --group_index {ES group} 
```

### Influence unlearning

```
python main_forget.py --unlearn wfisher --num_indexes_to_replace 3000 --alpha ${alpha} --mem {memorization group} --group_index {ES group} 
```


### SalUn

```
python generate_mask.py --save ${saliency_map_path} --num_indexes_to_replace 3000 --unlearn_epochs 1 --mem {memorization group} --group_index {ES group} 
```
```
python main_random.py --unlearn RL --unlearn_lr 0.1 --unlearn_epochs 10 --num_indexes_to_replace 3000 --path ${saliency_map_path} --mem {memorization group} --group_index {ES group} 
```

### Random-label

```
python main_random.py --unlearn RL_og --unlearn_lr 0.1 --unlearn_epochs 10 --num_indexes_to_replace 3000 --mem {memorization group} --group_index {ES group} 
```
### Get ToW / ToW-MIA

```
python analysis.py --dataset {dataset name} --arch {model architecture} --no_aug --unlearn ${unlearn method} --mem_proxy {memorization proxy} --mem {memorization group} --num_indexes_to_replace 3000
```
```
python analysis_mia.py --dataset {dataset name} --arch {model architecture} --no_aug --unlearn ${unlearn method} --mem_proxy {memorization proxy} --mem {memorization group} --num_indexes_to_replace 3000
```

# References
We have used the code from the following repositories:

[SalUn] (https://github.com/OPTML-Group/Unlearn-Saliency)

[SCRUB] (https://github.com/meghdadk/SCRUB)

[Heldout Influence Estimation] (https://github.com/google-research/heldout-influence-estimation)

[Data Metrics] (https://github.com/meghdadk/data-metrics)

We have also used the public pre-computed memorization for CIFAR-100 dataset from https://pluskid.github.io/influence-memorization/

