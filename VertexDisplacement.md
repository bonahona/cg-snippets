# Vertex displacement

All magic in a vertex displacement shader takes place in the vertex shader(obviously).
Most include manipulation of the vertex position put sometimes it also includes its normal and UV cordinates.

## Dipslace over time base on world position
```
void vert(inout appdata_full v) {
	half3  position = v.vertex.xyz;
	half3 offset = mul(unity_WorldToObject, sin(_Time.w));
	position.xz += (offset.xz * localStrength);	// Only move vertex along the XZ plane
	v.vertex.xyz = position;
}
```
![alt text](https://raw.githubusercontent.com/bonahona/cg-snippets/master/Images/VertexDisplacement.gif "Vertex displacement")