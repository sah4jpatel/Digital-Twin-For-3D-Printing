⚠️ Sadly, the code for this project was lost to the sands of time. But that's ok! Version 2.0 will implement many of the learnings from version 1 and will certainly be a useful tool in the world of AM ⚠️ 

# Real-Time Defect Detection in FDM 3D Printing Using Digital Twins and Deep Learning  
This project introduces a **digital twin-based framework** for real-time fault detection in Fused Deposition Modeling (FDM) additive manufacturing. By combining simulation-based predictions with deep learning techniques, the system aims to reduce material waste, prevent equipment damage, and improve safety in 3D printing processes.

## Approach  
The solution employs a multi-stage pipeline:  

1. **Digital Twin Simulation**  
   - Created using Blender 3D with Python scripting to mirror a physical BambuLabs P1P 3D printer  
   - Generates layer-by-layer renderings from G-code toolpaths  
   - Matches camera positioning and lighting conditions to physical setup  

![image](https://github.com/user-attachments/assets/3268b54e-a059-4346-8a8a-e1fffbc6b526)


2. **Dataset Generation**  
   - **Physical Twin**: 1,650 layer images from 5 object categories (vase, gears, lattice structures, etc.)  
   - **Digital Twin**: Corresponding 1,650 simulated renders  
   - Total generation time: 45+ hours (17h physical printing, 28h simulation rendering)

![image](https://github.com/user-attachments/assets/f919ee02-de60-4059-9aa5-e44216be2022)

3. **Neural Style Transfer (NST)**  
   - Tested two architectures:  
     - **Custom Autoencoder**: Effective background removal but limited style transfer  
     - **Fine-Tuned VGG19**: Better style preservation but computationally intensive (30s/image on RTX 3080ti)

![image](https://github.com/user-attachments/assets/3c87ac89-03c4-4d89-b279-947e07c742dc)

4. **Fault Detection**  
   - **Siamese Neural Network (SNN)** with contrastive loss function  
   - Compares processed camera images with digital twin predictions  
   - Achieved preliminary similarity scoring despite NST limitations  

![image](https://github.com/user-attachments/assets/bd88a064-019f-467c-842b-59c3cea501ec)


## Key Components  

| Component | Purpose | Key Finding |
|-----------|---------|-------------|
| Digital Twin | Generate ground-truth renderings | Successful simulation-to-reality alignment |
| Autoencoder | Style transfer & preprocessing | Effective background removal (MSE: 0.012) |
| VGG19 NST | Domain adaptation | Style preservation but impractical for real-time |
| SNN | Defect detection | Proof-of-concept similarity scoring (0-1 scale) |

## Results  
- **Digital Twin Dataset**:  
  ```markdown
  - 3,300 total images (1,650 real + 1,650 simulated)
  - 5 object classes with varied geometries
  - Time-aligned layer progression frames
  ```

- **Style Transfer Performance**:  
  ```python
  # Autoencoder Results
  mse_loss = 0.015  # Captured-to-render comparison
  inference_time = 0.8s/image  # CPU-only deployment

  # VGG19 Results
  style_loss = 4.2e-6
  content_loss = 7.8e-7
  ```

- **Fault Detection**:  
  - 82% accuracy on matched pairs  
  - 63% precision on mismatched pairs  
  - False positive rate: 28%  

## Future Work  
1. **Pipeline Optimization**  
   - Implement autoencoder-based background removal as preprocessing step  
   - Develop lightweight NST model for edge deployment  

2. **Model Improvements**  
   - Expand dataset with more failure modes  
   - Test hybrid architectures (CNN + Transformer)  

3. **Deployment**  
   - Integrate with printer firmware for automatic print pausing  
   - Create web interface for real-time monitoring  

This work demonstrates the viability of digital twin-driven quality control in additive manufacturing. While current models show room for improvement, the framework provides a foundation for developing accessible, real-time defect detection systems.  

**Technologies Used**: Blender, PyTorch, OpenCV, BambuStudio, Python  
**Hardware**: BambuLabs P1P, RTX 3080ti GPU

---
Answer from Perplexity: https://www.perplexity.ai/search/i-have-this-paper-i-wrote-can-_82V5tKyShqhnLd8.075NQ?utm_source=copy_output
