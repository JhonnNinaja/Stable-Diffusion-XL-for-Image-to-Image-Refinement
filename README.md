
## Stable Diffusion XL for Image-to-Image Refinement

This project leverages the Stable Diffusion XL model to transform and refine images, generating detailed and creative outputs.

**Dependencies:**

* **diffusers** - Library for working with diffusion models. 
* **transformers** - Provides natural language processing and machine learning models.
* **accelerate** - Optimizes deep learning model execution.
* **invisible_watermark** - (Optional) For adding invisible watermarks to your generated output.
* **mediapy** - (Optional) For handling various media formats.

**Installation**

```bash 
pip install --quiet --upgrade diffusers transformers accelerate invisible_watermark mediapy
``` 

**Set Up**

1. **Model Download:** The code automatically downloads the pre-trained Stable Diffusion XL model (stable-diffusion-xl-refiner-1.0).
2. **CUDA Compatibility:** Verify that your system has a CUDA-enabled GPU for hardware acceleration.

**Usage**

1.  **Provide an Input Image:**  Two methods to provide an input image:
    *   **URL:**  Fetch an image from a URL.  
       ```python
        url = "https://raw.githubusercontent.com/CompVis/stable-diffusion/main/assets/stable-samples/img2img/sketch-mountains-input.jpg"
        response = requests.get(url)
        init_img = Image.open(BytesIO(response.content)).convert("RGB")
        ```
    *    **Local File:**  Upload your image directly.
        ```python
        init_img = Image.open("/content/Captura de pantalla 2023-08-12 142056.png") 
        ``` 
2. **Resize Image (Optional):**
   ```python
    width, height = init_img.size
    new_width = 700
    aspect_ratio = height / width
    new_height = int(aspect_ratio * new_width)
    init_img = init_img.resize((new_width, new_height))
   ```

3. **Define Prompts:** Use descriptive text prompts to guide the image modification:
   ```python
    prompt = "vectorized key chain, illustration, text, 3d printed"
    prompt_logo = "Logo for a condor company,blue-green,a condor, come to life,symmetrical,wild nature,illustration,vector art,logo design, text"
   ```

4. **Run the Model:**
    ```python
    image = pipe(prompt=prompt, 
                 image=init_img, 
                 strength=0.75, # Adjust transformation strength (0-1)
                 guidance_scale=7.5, # Adjust how closely the output follows the prompt
                 generator=torch.Generator("cuda").manual_seed(seed)).images[0] 
    image.save("output.png") 
    ```

**Example**

![Imagen del proyecto](./download.png) --> ![Imagen del proyecto](./download(1).png)


