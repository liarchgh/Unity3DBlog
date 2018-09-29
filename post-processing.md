# [Post-processing](https://docs.unity3d.com/Packages/com.unity.postprocessing@2.0/manual/index.html)

官方`Package Manager`里面的插件

## 简单说明

- 需要添加后处理效果的`Camera`上添加组件

- 给物体添加`Post Process Volume`组件
    - Global
    
        可以挂在任意物体上，效果相同
        
    - Not Global
    
        需要挂在有`Collider`或`Trigger`的物体上，这两个组件的范围即是触发
        
## Component

### Post Process Layer

- Volume blending

    - Trigger
    
    - Layer
    
- Anti-aliasing

    - Mode
    
    - Stop NaN Propagation
    
- Depth Of Field

    - Auto Focus
    
- Toolkit

    - Exportframe to EXR...
    
        - Full Frame(as displayed)
        
        - Disable post-processing
        
        - Break before Color Grading(Linear)
        
        - Break before Color Grading(Log)
    
    - Select all layer volumes
    
    - Select all active volumes
    
- Custom Effect Sorting

### Post Process Volume

- Is Global

- Blend Distance

- Weight

- Priority

- Profile

- Overrides

    - Add effect...
    
        - Unity
        
            - Ambient Occlusion
            
            - Auto Exposure
            
            - Bloom
            
            - Chromatic Aberration
            
            - Color Grading
            
            - Depth of Field
            
                - Focus Distance
                
                - Aperture
                
                - Focal Length
                
                - Max Blur Size
            
            - Grain
            
            - Lens Destortion
            
            - Motion Blur
            
            - Screen-space reflections
            
            - Vignette