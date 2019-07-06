# Vertex displacement

All magic in a vertex displacement shader takes place in the vertex shader(obviously).
Most include manipulation of the vertex position put sometimes it also includes its normal and UV cordinates.

## Displace over time based on world position
```
void vert(inout appdata_full v) {
	half3  position = v.vertex.xyz;
	half3 offset = mul(unity_WorldToObject, sin(_Time.w));
	position.xz += (offset.xz * localStrength);	// Only move vertex along the XZ plane
	v.vertex.xyz = position;
}
```
![alt text](https://raw.githubusercontent.com/bonahona/cg-snippets/master/Images/VertexDisplacement.gif "Vertex displacement")

## Displacement based on model space

Displaces vertex in its (local) YZ plane base on its distance from origo in model space.

```
void vert(inout appdata_full v){
	float3 position = v.vertex.xyz;
	float amplitude = 0.001 * _Amplitude * abs(position.y);
	float waves = 2 * UNITY_PI / _WaveLength;

	float ofset = waves * (position.y + _Time.w * _Speed);
	float3 tangent = normalize(float3(1, waves * amplitude * cos(ofset), 0));
	float3 normal = float3(-tangent.y, tangent.x, 0);

	position.z = (sin(ofset) - 0.75) * amplitude ;

	v.vertex.xyz = position;
	v.normal = normal;
}
```
![alt text](https://raw.githubusercontent.com/bonahona/cg-snippets/master/Images/VertexDisplacementFlags.gif "Vertex displacement")

## Displace based on normals
Displaces the vertex "forward" based on their normal direction.

(This shader also uses a grab pass display the underlying render buffer displaced and heavy alpha in the middle (with a Rim effect) to display the underlying render buffer unaltered).
```
half4 pos = UnityObjectToClipPos(v.vertex);
o._uvGrabTex = ComputeGrabScreenPos(pos);
float3 worldPos = mul (unity_ObjectToWorld, v.vertex).xyz;
v.vertex.xyz += v.normal * sin((_Time * 5) + worldPos.xyz) * 0.1;
```
![alt text](https://raw.githubusercontent.com/bonahona/cg-snippets/master/Images/VertexDisplacementNormal.gif "Vertex displacement")