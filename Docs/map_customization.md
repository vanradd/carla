# Map customization

This are the specific blueprint assets created to help building the environment.

## MultipleFloorBuilding:

The purpose of this blueprint is to make repeating and varying tall buildings a bit easier. Provided a Base, a MiddleFloor and a roof; this blueprint repeats the middle floor to the desired number of stores and tops it whith the last floor given some conditions:
  - All model pivots should be in the bottom center of the Specific mesh.
  - Al models must start and end exactly where the repetition happen.

This blueprint is controlled by this 6 specific Parameters:

  - GroundFloor: The mesh to be placed in the base of the building.
  - Floor: The mesh to be repeated along the building.
  - Roof: Final mesh to top the building.
  - FloorNumber: Number of stores of the building.
  - FloorHeightOffset: Adjust The placement of every floor verticaly.
  - RoofOffset: Adjust the placement of the roof verticaly.

All of This parameters can be modified once this blueprint is placed in the world.

## SplinemeshRepeater:

!!! Bug
    See [#35 SplineMeshRepeater loses its collider mesh](https://github.com/carla-simulator/carla/issues/35)
    
### Standard use:

SplineMeshRepeater "Content/Blueprints/SplineMeshRepeater" is a tool included in the Carla Project to help building urban environments; It repeats and aligns a specific choosen mesh along a [Spline](https://docs.unrealengine.com/latest/INT/Engine/BlueprintSplines/Reference/SplineEditorTool/index.html) (Unreal Component). Its principal function is to build Tipicaly tiled and repetitive structures as Walls, Roads, Bridges, Fences... Once the actor is placed into the world the spline can be modified so the object gets the desired form. Each Point Defining the spline Generates a new tile so that as more points the Spline has, the more defined it will be, but also heavyer on the world. This actor is defined by the following parameters:


  - StaticMesh: The mesh to be repeated along the spline.
  - ForWardAxis: Changes the mesh axis to be alingned with the spline.
  - Material: Overrides the mesh' default material.
  - Colission Enabled: Chooses the tipe of colission to use.
  - Gap distance: Places a Gap between each repeated mesh, for repetitive non continuous walls: bush chains, bollards...


(Last three variables are specific for some particular assets to be defined in the next point) A requisite to create assets compatibles with this componenis is that all the meshes have their pivot placed wherever the repetition starts in the lower point possible with the rest of the mesh pointing positive (Preferably by the X axis)


### Specific Walls (Dynamic material)

In the project folder "Content/Static/Walls" are included some specific assets to be used with this SplineMeshRepeater with a series of special caracteristics. The uv space of this meshes and their materials are the same for all of them, making them excangeable. each material is composed of three different surfaces the last three parameters slightly modify the color of this surfaces:

  - MainMaterialColor: Change the main material of the Wall
  - DetailsColor: Change the color of the details (if any)
  - TopWallColor: Cambia el color de la cubierta del muro (if any)

   To add elements that profit from this functions exist in the (Carpeta) folder the GardenWallMask File that defines the uv space to place the materials: (Blue space: MainMaterial; green space: Details; red space TopWall).

Between the material masters is WallMaster which is going to be the master of the materials using this function. An instance of this material will be created and the correspondent textures will be added. This material includes the following parameters to be modified by the material to use:

  - Normal Flattener: Slightly modifies the normal map values to exagerate it or flatten it.
  - RoughnessCorrection: Para corregir El valor de rugosidad dado por la textura.

  The rest of the parameters are the mask the textures and the color corrections that won't be modified in this instance but in the blueprint that will be launched into the world.




## Weather
This is the actor in charge of modifying all the lighting, environmental actors an anything that affects the impression of the climate. It runs automaticaly with the game when is not specified otherwise In the Config.Ini but has Its own actor to launch in editor mode to configure the climatic conditions. To fuly work It will need One of each of the folowing actors: SkySphere, Skylight, Postprocess Volume (Boundless) And Light Source to exist in the world.

  - SunPolarAngle: polar angle of the sun, determines time of the day
  - SunAzimuthAngle: adds to the location of the sun in the current level
  - SunBrightness: Brightness of the rendering of the sun in the skybox
  - SunDirectionalLightIntensity: Intensity of the sunlight
  - SunDirectionalLightColor: Color of the sunlight
  - SunIndirectLightIntensity: intensity of the bounces of the main light
  - CloudOpacity: visivility of the cloud rendering on the skybox
  - HorizontFalloff: determines the height of the gradient between the zenith and horizon color
  - ZenithColor: Defines the color of the zenith.
  - HorizonColor: Defines the color of the horizon.
  - CloudColor: Defines the color of the Clouds, if any.
  - OverallSkyColor: multiplies every colored element in the sky by a single color.
  - SkyLightIntensity: Intensity of the light bounced from the sky.
  - SkyLightColor: Color of the light bounced from the sky.
  - Precipitation: Defines if any precipitation is active.
  - PrecipitationType: the type of precipitation to active.
  - PrecipitationAmount: the quantity of the chosen precipitation.
  - PrecipitationAccumulation: the acumulation of the chosen precipitation.
  - bWind: defines if there is any wind.
  - WindIntensity: defines the wind intensity.
  - WindAngle: defines the wind direction.
  - bOverrideCameraPostProcessParameters: Defines if the default camera postprocess is overwritten.
  - CameraPostProcessParameters.AutoExposureMethod: Defines the method of autoexposure.
  - CameraPostProcessParameters.AutoExposureMinBrightness: defines the minimum brightness the autoexposure will count as right in the final image.
  - CameraPostProcessParameters.AutoExposureMaxBrightness: defines the maximum brightness the autoexposure will count as right in the final image.
  - CameraPostProcessParameters.AutoExposureBias: Darkens or brightens the final image towards a defined bias.


You can have as many different configurations saved in the proyect as you want and choose the configuration to aply while on the build, through the [settings file](carla_settings.md); or in the editor while building the level or testing.