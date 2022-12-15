# Creative Title Generator

## Motivation

It goes without saying that the title of any article is important to attract people's attention. Currently, there are various title generators, but they are all extracted based on keywords. Input text, create a title, and measure accuracy based on how similar it is to the actual title. However, this method can only extract formal titles, and it is not enough to make creative and eye-catching titles. So we wanted to create a Title Generator that would create a more creative title.

## Get started

1. Create docker container with docker-compose

```bash
docker compose up -d
docker compose exec dev bash
```

2. Install dependencies

```bash
# In container
pip install -U -r requirements.txt
accelerate config
huggingface-cli login
```

3. Set environment variables

```bash
export MODEL_NAME="CompVis/stable-diffusion-v1-4"
export dataset_name="amazon_reviews_multi"
```

4. Build and train model

```bash
accelerate launch train_text_to_image.py \
  --pretrained_model_name_or_path=$MODEL_NAME \
  --dataset_name=$dataset_name \
  --train_batch_size=4 \
  --gradient_accumulation_steps=1 \
  --gradient_checkpointing \
  --mixed_precision="fp16" \
  --max_train_steps=10000 \
  --learning_rate=1e-05 \
  --max_grad_norm=1 \
  --lr_scheduler="constant" --lr_warmup_steps=1000 \
  --output_dir="output/text-ldm"
```
