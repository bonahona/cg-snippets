// Data send between vertex and surface/fragment shader needed to be added
struct Input {
	float3 worldNormal;
	float3 viewDir;
};

// Calculate rim effect
float border = 1 - (abs(dot(IN.viewDir, IN.worldNormal)));
float alpha = (border * (1 - _DotProduct) + _DotProduct);

// Alternative (smoother) rimeffect)
float border = 1 - (dot(IN.worldNormal, IN.viewDir));
float rimFactor = pow(border, _RimEffect);
float alpha = border;
