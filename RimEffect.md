# Rim effect shaders

## Generic setup
In order to get these rim efefct shaders to work, extent the Input (v2f) struct with worldNormal and viewDir variables.
Unity will automatically populate these once added.
```
struct Input {
	float3 worldNormal;
	float3 viewDir;
};
```

## Variant 01
```
float border = 1 - (abs(dot(IN.viewDir, IN.worldNormal)));
float alpha = (border * (1 - _DotProduct) + _DotProduct);
```
![alt text](https://raw.githubusercontent.com/bonahona/cg-snippets/master/Images/ManaShieldShow.gif "Rim effect variant 01")
(As you migh guess this example also uses some UV offsetting for its effect.)

## Variant 02
Alternative (smoother) rimeffect.
'_RimEffect' is a fixed with an expected range of 0 - 10 and sets how strong the effet should be.
```
float border = 1 - (dot(IN.worldNormal, IN.viewDir));
float rimFactor = pow(border, _RimEffect);
float alpha = border;
```
![alt text](https://raw.githubusercontent.com/bonahona/cg-snippets/master/Images/SpectralDaggerShow.gif "Rim effect variant 01")
