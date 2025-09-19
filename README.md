
# AdSnap: AI-Powered Ad Banner Generator

## Project Overview  
This project automates advertisement banner generation, by implementing a modular AI powered advertisement banner generation pipeline, which transforms raw inputs like product image, tone input, product name into visually coherent and lightweight banners. 

Our modular architecture provides flexibility and interpretability for the entire pipeline – from slogan generation to dynamic color contrast, font sizing, textbox selection and background color analysis. 

This system: 
- Loads product images + product name + tone + annotations
- Uses LLM to generate catchy tone-aware slogans 
- Finds the largest bounding box by for rendering the slogan
- Font color is decided based on background brightness
- Adds a CTA banner at the bottom: with a CTA button, price, tagline
- The background color for CTA is based on the bottom 15% color of poster

## Dataset
It uses the Creative Graphic Layout (CGL) Dataset from HuggingFace, which contains 60,000+ records about:
            •	image – A product image (PIL image object)
            •	text_features – A dictionary with key “pos”, which contains positions of bounding boxes for text, logo, and price
            •	annotations – COCO annotations with fields like category, bbox, segmentation, etc.
            •	Image_id
            •	File_name 
            •	text_annotations –OCR-related text recognition fields (not used in this project)
            

## Dependencies  

Install the required packages with:

```bash
pip install openai python-dotenv datasets pillow opencv-python matplotlib numpy
---
Other built-in Python modules used in this project are: random, os, time, ast, IPython.display

## 🔑 Setup OpenAI API  
1. Generate a OpenAI key
2. Create a `.env` file in the root folder  
3. Add your OpenAI key like this:  
```
OPENAI_API_KEY=sk-xxxxxx
```

The notebook will automatically load this key using the code added. This ensures your key is safe. 
Do not paste your key directly in the notebook.

---

## How to Run  
1. Launch Jupyter Notebook
```bash
jupyter notebook AdSnap.ipynb
```

2. Run all cells:
- It will load the `CGL-Dataset-v2` from HuggingFace
- Extract bounding box annotations
- Assign product names and tones manually (for first 50 entries)
- Generate 3 slogans using GPT-3.5, select the best one
- Place slogan in the largest box 
- Decides text color based on background
- Background color for CTA is based on the bottom 15% color of poster
- Adds CTA banner at the bottom

---

## Example Outputs  
Each final image includes:
-  Catchy tone-aligned slogan rendered in largest bounding box
-  CTA banner
-  contrast-aware text rendering
---

## Known Limitations  
- Dataset does not contain product name and tone, so these were added manually by randomly selecting through code  
- CTA is fixed logic
- Tone based styling not present
- Text may occasionally overlap image content

---

## Troubleshooting  
             
Problem: OpenAI error 
Solution: Check `.env` file and API key        

Problem: Dataset download fails    	
Solution: Ensure you have internet connection. It is a huge dataset and might take a lot of time and stable internet. Alternatively you can skip the cell and only use the streaming version in the next cell 

---

## Future Enhancements  
- Tone style transfer
- Quantitative evaluation pipeline with user feedback to improve quality and provide refinement. 
- Eye tracking inspired layout
- Product name recognition using OCR  


