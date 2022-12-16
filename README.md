# Text style transfer with LDM


## Finetune example with image dataset

```bash
pip install -U -r requirements.txt
accelerate config
huggingface-cli login
```

```bash
export MODEL_NAME="CompVis/stable-diffusion-v1-4"
export dataset_name="amazon_reviews_multi"

accelerate launch train_text_to_text.py \
  --pretrained_model_name_or_path=$MODEL_NAME \
  --dataset_name=$dataset_name \
  --train_batch_size=4 \
  --gradient_accumulation_steps=1 \
  --gradient_checkpointing \
  --mixed_precision="fp16" \
  --max_train_steps=10000 \
  --learning_rate=1e-05 \
  --max_grad_norm=1 \
  --lr_scheduler="constant" --lr_warmup_steps=0 \
  --output_dir="output/text-ldm"
```
