# 3dlib-three.js —— 3d引擎库之three.js源码分析

#### 源码分析的动力来源

随着前端在AR/VR领域的渗透，越来越多的webgl引擎库出现，前端在实现3D效果时，如何选择一个合适的引擎库以及对比各个引擎库的优缺点，对引擎库的源码分析是一件非常有意义的事情。

#### 引擎库模块结构 ###

```
src
|
  | Three.Legacy.js
  | Three.js
  | constants.js
  | polyfills.js
|
--cameras
|
  | Camera.js
  | CubeCamera.js
  | OrthographicCamera.js
  | PerspectiveCamera.js
  | StereoCamera.js
|
--core
|
  | BufferAttribute.js
  | BufferGeometry.js
  | Clock.js
  | DirectGeometry.js
  | EventDispatcher.js
  | Face3.js
  | Geometry.js
  | InstancedBufferAttribute.js
  | InstancedBufferGeometry.js
  | InstancedInterleavedBuffer.js
  | InterleavedBuffer.js
  | InterleavedBufferAttribute.js
  | Layers.js
  | Object3D.js
  | Raycaster.js
  | Uniform.js
|
--extras
|
  | CurveUtils.js
  | SceneUtils.js
  | ShapeUtils.js
  |
  |--core
  |
    | Curve.js
    | CurvePath.js
    | Font.js
    | Path.js
    | PathPrototype.js
    | Shape.js
  |
  |--curves
    | 
    | ArcCurve.js
    | CatmullRomCurve3.js
    | CubicBezierCurve3.js
    | CubicBezierCurve3.js
    | EllipseCurve.js
    | LineCurve.js
    | LineCurve3.js
    | QuadraticBezierCurve.js
    | QuadraticBezierCurve3.js
    | SplineCurve.js
    | SplineCurve3.js
  | 
  |--helpers
    |
    | ArrowHelper.js
    | AxisHelper.js
    | BoxHelper.js
    | CameraHelper.js
    | DirectionalLightHelper.js
    | FaceNormalsHelper.js
    | GridHelper.js
    | HemisphereLightHelper.js
    | PointLightHelper.js
    | PolarGridHelper.js
    | RectAreaLightHelper.js
    | SkeletonHelper.js
    | SpotLightHelper.js
    | VertexNormalsHelper.js
  |
  |--objects
    |
    | ImmediateRenderObject.js
    | MorphBlendMesh.js
  | 
--geometries
  |
  | BoxBufferGeometry.js
  | BoxGeometry.js
  | CircleBufferGeometry.js
  | CircleGeometry.js
  | ConeBufferGeometry.js
  | ConeGeometry.js
  | CylinderBufferGeometry.js
  | CylinderGeometry.js
  | DodecahedronBufferGeometry.js
  | DodecahedronGeometry.js
  | EdgesGeometry.js
  | ExtrudeGeometry.js
  | Geometries.js
  | IcosahedronBufferGeometry.js
  | IcosahedronGeometry.js
  | LatheBufferGeometry.js
  | LatheGeometry.js
  | OctahedronBufferGeometry.js
  | OctahedronGeometry.js
  | ParametricBufferGeometry.js
  | ParametricGeometry.js
  | PlaneBufferGeometry.js
  | PlaneGeometry.js
  | PolyhedronGeometry.js
  | RingBufferGeometry.js
  | RingGeometry.js
  | ShapeBufferGeometry.js
  | ShapeGeometry.js
  | SphereBufferGeometry.js
  | SphereGeometry.js
  | TetrahedronBufferGeometry.js
  | TetrahedronGeometry.js
  | TextGeometry.js
  | TorusBufferGeometry.js
  | TorusGeometry.js
  | TorusKnotBufferGeometry.js
  | TorusKnotGeometry.js
  | TubeBufferGeometry.js
  | TubeGeometry.js
  | WireframeGeometry.js
|
--lights
  |
  | AmbientLight.js
  | DirectionalLight.js
  | DirectionalLightShadow.js
  | HemisphereLight.js
  | Light.js
  | LightShadow.js
  | PointLight.js
  | RectAreaLight.js
  | RectAreaLightShadow.js
  | SpotLight.js
  | SpotLightShadow.js
  |
--loaders
  |
  | AnimationLoader.js
  | AudioLoader.js
  | BinaryTextureLoader.js
  | BufferGeometryLoader.js
  | Cache.js
  | CompressedTextureLoader.js
  | CubeTextureLoader.js
  | FileLoader.js
  | FontLoader.js
  | ImageLoader.js
  | JSONLoader.js
  | Loader.js
  | LoadingManager.js
  | MaterialLoader.js
  | ObjectLoader.js
  | TextureLoader.js
 |
--materials
  |
  | LineBasicMaterial.js
  | LineDashedMaterial.js
  | Material.js
  | Materials.js
  | MeshBasicMaterial.js
  | MeshDepthMaterial.js
  | MeshLambertMaterial.js
  | MeshNormalMaterial.js
  | MeshPhongMaterial.js
  | MeshPhysicalMaterial.js
  | MeshStandardMaterial.js
  | MeshToonMaterial.js
  | MultiMaterial.js
  | PointsMaterial.js
  | RawShaderMaterial.js
  | ShaderMaterial.js
  | ShadowMaterial.js
  | SpriteMaterial.js
  |
--math
  |
  |--interpolants
  |
    | CubicInterpolant.js
    | DiscreteInterpolant.js
    | LinearInterpolant.js
    | QuaternionLinearInterpolant.js
  |
  | Box2.js
  | Box3.js
  | Color.js
  | Cylindrical.js
  | Euler.js
  | Frustum.js
  | Interpolant.js
  | Line3.js
  | Math.js
  | Matrix3.js
  | Matrix4.js
  | Plane.js
  | Quaternion.js
  | Ray.js
  | Sphere.js
  | Spherical.js
  | Spline.js
  | Triangle.js
  | Vector2.js
  | Vector3.js
  | Vector4.js
  |
--objects
  |
  | Bone.js
  | Group.js
  | LOD.js
  | LensFlare.js
  | Line.js
  | LineSegments.js
  | Mesh.js
  | Points.js
  | Skeleton.js
  | SkinnedMesh.js
  | Sprite.js
  |
--renderers
  |
  |--shaders
|   |
|   |--ShaderChunk
|   | alphamap_fragment.glsl
|   | alphamap_pars_fragment.glsl
|   | alphatest_fragment.glsl
|   | aomap_fragment.glsl
|   | aomap_pars_fragment.glsl
|   | begin_vertex.glsl
|   | beginnormal_vertex.glsl
|   | bsdfs.glsl
|   | bumpmap_pars_fragment.glsl
|   | clipping_planes_fragment.glsl
|   | clipping_planes_pars_fragment.glsl
|   | clipping_planes_pars_vertex.glsl
|   | clipping_planes_vertex.glsl
|   | color_fragment.glsl
|   | color_pars_fragment.glsl
|   | color_pars_vertex.glsl
|   | color_vertex.glsl
|   | common.glsl
|   | cube_uv_reflection_fragment.glsl
|   | defaultnormal_vertex.glsl
|   | displacementmap_pars_vertex.glsl
|   | displacement_vertex.glsl
|   | emissivemap_fragment.glsl
|   | emissivemap_pars_fragment.glsl
|   | encodings_fragment.glsl
|   | encodings_pars_fragment.glsl
|   | envmap_fragment.glsl
|   | envmap_pars_fragment.glsl
|   | envmap_pars_vertex.glsl
|   | envmap_vertex.glsl
|   | fog_fragment.glsl
|   | fog_pars_fragment.glsl
|   | gradientmap_pars_fragment.glsl
|   | lightmap_fragment.glsl
|   | lightmap_pars_fragment.glsl
|   | lights_lambert_vertex.glsl
|   | lights_pars.glsl
|   | lights_phong_fragment.glsl
|   | lights_phong_pars_fragment.glsl
|   | lights_physical_fragment.glsl
|   | lights_physical_pars_fragment.glsl
|   | lights_template.glsl
|   | lights_template.glsl
|   | logdepthbuf_fragment.glsl
|   | logdepthbuf_pars_fragment.glsl
|   | logdepthbuf_pars_vertex.glsl
|   | logdepthbuf_vertex.glsl
|   | map_fragment.glsl
|   | map_pars_fragment.glsl
|   | map_particle_fragment.glsl
|   | map_particle_pars_fragment.glsl
|   | metalnessmap_fragment.glsl
|   | metalnessmap_pars_fragment.glsl
|   | morphnormal_vertex.glsl
|   | morphtarget_pars_vertex.glsl
|   | morphtarget_vertex.glsl
|   | normal_flip.glsl
|   | normal_fragment.glsl
|   | normalmap_pars_fragment.glsl
|   | packing.glsl
|   | premultiplied_alpha_fragment.glsl
|   | project_vertex.glsl
|   | roughnessmap_fragment.glsl
|   | roughnessmap_pars_fragment.glsl
|   | shadowmap_pars_fragment.glsl
|   | shadowmap_pars_vertex.glsl
|   | shadowmap_vertex.glsl
|   | shadowmask_pars_fragment.glsl
|   | skinbase_vertex.glsl
|   | skinning_pars_vertex.glsl
|   | skinning_vertex.glsl
|   | skinnormal_vertex.glsl
|   | specularmap_fragment.glsl
|   | specularmap_pars_fragment.glsl
|   | tonemapping_fragment.glsl
|   | tonemapping_pars_fragment.glsl
|   | uv2_pars_fragment.glsl
|   | uv2_pars_vertex.glsl
|   | uv2_vertex.glsl
|   | uv_pars_fragment.glsl
|   | uv_pars_vertex.glsl
|   | uv_vertex.glsl
|   | worldpos_vertex.glsl
| |
| |--ShaderLib
| |
|   | cube_frag.glsl
|   | cube_vert.glsl
|   | depth_frag.glsl
|   | depth_vert.glsl
|   | distanceRGBA_frag.glsl
|   | distanceRGBA_vert.glsl
|   | equirect_frag.glsl
|   | equirect_vert.glsl
|   | linedashed_frag.glsl
|   | linedashed_vert.glsl
|   | meshbasic_frag.glsl
|   | meshbasic_vert.glsl
|   | meshlambert_frag.glsl
|   | meshlambert_vert.glsl
|   | meshphong_frag.glsl
|   | meshphong_vert.glsl
|   | meshphysical_frag.glsl
|   | meshphysical_vert.glsl
|   | normal_frag.glsl
|   | normal_vert.glsl
|   | points_frag.glsl
|   | points_vert.glsl
|   | shadow_frag.glsl
|   | shadow_vert.glsl
| |
| | ShaderChunk.js
| | ShaderLib.js
| | UniformsLib.js
| | UniformsUtils.js
| |
| |--webgl
|   |--plugins
|     | LensFlarePlugin.js
|     | SpritePlugin.js
|   |
|   | WebGLBufferRenderer.js
|   | WebGLCapabilities.js
|   | WebGLClipping.js
|   | WebGLExtensions.js
|   | WebGLGeometries.js
|   | WebGLIndexedBufferRenderer.js
|   | WebGLLights.js
|   | WebGLObjects.js
|   | WebGLProgram.js
|   | WebGLPrograms.js
|   | WebGLProperties.js
|   | WebGLShader.js
|   | WebGLShadowMap.js
|   | WebGLState.js
|   | WebGLTextures.js
|   | WebGLUniforms.js
| |
| | WebGL2Renderer.js
| | WebGLRenderTarget.js
| | WebGLRenderTargetCube.js
| | WebGLRenderer.js
|
|--scenes
|
  | Fog.js
  | FogExp2.js
  | Scene.js
|
|--textures
|
  | CanvasTexture.js
  | CompressedTexture.js
  | CubeTexture.js
  | DataTexture.js
  | DepthTexture.js
  | Texture.js
  | VideoTexture.js
|
| Three.Legacy.js
| Three.js
| constants.js
| polyfills.js

```
