// All magic in a vertex displacement shader takes place in the vertex shader(obviously).
void vert(inout appdata_full v) {
	half3  position = v.vertex.xyz;
	half3 offset = mul(unity_WorldToObject, sin(_Time.w));
	position.xz += (offset.xz * localStrength);	// Only move vertex along the XZ plane
	v.vertex.xyz = position;
}