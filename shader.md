# Shader
## 时间
_Time float4 Time (t/20, t, t*2, t*3), use to animate things inside the shaders.

_SinTime float4 Sine of time: (t/8, t/4, t/2, t).

_CosTime float4 Cosine of time: (t/8, t/4, t/2, t).

unity_DeltaTime float4 Delta time: (dt, 1/dt, smoothDt, 1/smoothDt).  
 _Time.x = time / 20  
 _Time.y = time  
 _Time.z = time * 2  
 _Time.w = time * 3  