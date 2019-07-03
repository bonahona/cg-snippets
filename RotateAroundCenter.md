# Rotates around the center 

```
float2 pivot = float2(0.5, 0.5);
// Rotation Matrix
float cosAngle = cos(_Time.x * _Rotation);
float sinAngle = sin(_Time.x * _Rotation);
float2x2 rot = float2x2(cosAngle, -sinAngle, sinAngle, cosAngle);

// Rotation consedering pivot
float2 uv2 = i.uv - pivot;
i.uv = mul(rot, uv2);
i.uv += pivot;
i.uv = clamp(i.uv, 0, 1);
```
![alt text](https://raw.githubusercontent.com/bonahona/cg-snippets/blob/master/Images/Rotation.gif "Rotation effect")

If you plan on doing effects like this I strongly suggest just rotation the game object instead.