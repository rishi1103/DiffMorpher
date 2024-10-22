# How to run the code

## Setup

Open a Colab Notebook or choose an environment to do the setup. This README file will primarily focus on implementation
keeping Colab Notebook in mind.

Note: You should use a GPU for the colab notebook to run the code successfully

### Step 1

Clone the code into your disc using the following following command

```bash
!git clone https://github.com/rishi1103/DiffMorpher.git
```

After cloning is complement move to the code directory using 

```bash
%cd DiffMorpher
```

For installing the requirements for the code, use the following pip command

```bash
!pip install -r requirements.txt
```

After installation, Google Colab might prompt you to restart the runtime in order to incorporate the newly downloaded
libraries, simply restart the runtime and move back to original code directory using `%cd DiffMorpher`

To run the code use the following template

```bash
python main.py \
  --image_path_0 [image_path_0] --image_path_1 [image_path_1] \ 
  --prompt_0 [prompt_0] --prompt_1 [prompt_1] \
  --output_path [output_path] \
  --use_adain --use_reschedule --save_inter
```

These are the options supported for running

- `--image_path_0`: Path of the first image (default: "")
- `--prompt_0`: Prompt of the first image (default: "")
- `--image_path_1`: Path of the second image (default: "")
- `--prompt_1`: Prompt of the second image (default: "")
- `--model_path`: Pretrained model path (default: "stabilityai/stable-diffusion-2-1-base")
- `--output_path`: Path of the output image (default: "")
- `--save_lora_dir`: Path of the output lora directory (default: "./lora")
- `--load_lora_path_0`: Path of the lora directory of the first image (default: "")
- `--load_lora_path_1`: Path of the lora directory of the second image (default: "")
- `--use_adain`: Use AdaIN (default: False)
- `--use_reschedule`: Use reschedule sampling (default: False)
- `--lamb`: Hyperparameter $\lambda \in [0,1]$ for self-attention replacement, where a larger $\lambda$ indicates more replacements (default: 0.6)
- `--fix_lora_value`: Fix lora value (default: LoRA Interpolation, not fixed)
- `--save_inter`: Save intermediate results (default: False)
- `--num_frames`: Number of frames to generate (default: 50)
- `--duration`: Duration of each frame (default: 50)


Basically, after the code runs successfully the result folder will contain a gif file that transform the image in image_path_1 to the image in image_path_2.
The prompts for these images should be somewhat the explanation of the image stored.

When running the code, it will train our stable diffusion model on the given images and use the trained model to get the intermediate images.

Here are some example commands:

Examples:
```bash
python main.py \
  --image_path_0 ./assets/Trump.jpg --image_path_1 ./assets/Biden.jpg \ 
  --prompt_0 "A photo of an American man" --prompt_1 "A photo of an American man" \
  --output_path "./results/Trump_Biden" \
  --use_adain --use_reschedule --save_inter
```

```bash
python main.py \
  --image_path_0 ./assets/vangogh.jpg --image_path_1 ./assets/pearlgirl.jpg \ 
  --prompt_0 "An oil painting of a man" --prompt_1 "An oil painting of a woman" \
  --output_path "./results/vangogh_pearlgirl" \
  --use_adain --use_reschedule --save_inter
```

```bash
python main.py \
  --image_path_0 ./assets/lion.png --image_path_1 ./assets/tiger.png \ 
  --prompt_0 "A photo of a lion" --prompt_1 "A photo of a tiger" \
  --output_path "./results/lion_tiger" \
  --use_adain --use_reschedule --save_inter
```

## Results

The results can be found in the following pdf, along with dataset and implementation details: https://drive.google.com/drive/folders/1GKEDPHJZAfAIezL2PixeREHYsVmwAJgq?usp=drive_link

## MorphBench
To evaluate the effectiveness of our methods, we present *MorphBench*, the first benchmark dataset for assessing image morphing of general objects. You can download the dataset from [Google Drive](https://drive.google.com/file/d/1NWPzJhOgP-udP_wYbd0selRG4cu8xsu4/view?usp=sharing) or [Baidu Netdisk](https://pan.baidu.com/s/1J3xE3OJdEhKyoc1QObyYaA?pwd=putk).


## License
The code related to the DiffMorpher algorithm is licensed under [LICENSE](LICENSE.txt). 

However, this project is mostly built on the open-sourse library [diffusers](https://github.com/huggingface/diffusers), which is under a separate license terms [Apache License 2.0](https://github.com/huggingface/diffusers/blob/main/LICENSE). (Cheers to the community as well!)

## Citation

```bibtex
@article{zhang2023diffmorpher,
    title={DiffMorpher: Unleashing the Capability of Diffusion Models for Image Morphing},
    author={Zhang, Kaiwen and Zhou, Yifan and Xu, Xudong and Pan, Xingang and Dai, Bo},
    journal={arXiv preprint arXiv:2312.07409},
    year={2023}
}
```
