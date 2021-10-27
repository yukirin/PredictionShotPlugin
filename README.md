# [UE4 Marketplace] PredictionShotPlugin
[UE4 Marketplace] Prediction Shot Plugin Document  
[Marketplace URL](https://www.unrealengine.com/marketplace/prediction-shot-plugin)
# Tutorial
## Basic Tutorial
![BasicTutorial](https://github.com/yukirin/PredictionShotPlugin/blob/bb1c46ed6f0bd2851af09f511c385973d0644d8d/images/basic_tutorial.png "Basic Tutorial")
# Changelog
## Version 1.2
- Optimized processing when the predicted position collides with a wall etc.
- Add SetAccuracy Node (Ability to change Accuracy at runtime)
## Version 1.1
- Add PredictPos function to calculate predicted position
- Add HighArc option to shoot projectiles such as grenades at a higher angle
- Improve accuracy of prediction calculation during circular movement
- BugFix prediction calculation during counterclockwise circular movement
# Correspondence table of FCSComponent and MeasurerComponent
Measurer components that can be attached per FCS component are different

 |FCS Component|Mesurer Component|
 |---|---|
 |LinearFCS|{SMA, EMA} VelocityMeasurer|
 |CircularFCS|{SMA, EMA} AngularMeasurer|
 |CharacterLinearFCS|{SMA, EMA} VelocityMeasurer|
 |CharacterCircularFCS|{SMA, EMA} AngularMeasurer|

# Blueprint API Reference
## {Linear, CharacterLinear} FCS SceneComponent
### `Variables`

 |Type|Name|Description|
 |--:|---|---|
 |int32|Accuracy|Accuracy of prediction calculation|
 |float|ObserverTickInterval|Observe the target at the interval|
 |ECollisionChannel|TraceChannel|Trace channel for measuring the height of the landing point|
 |float|OffsetFromCollisionSurface|Offset value when the predicted point collides with the surface (Default = 50)|
 |IVelocityObservable|Observer|Object implementing IVelocityObservable|
 
### `Functions`

 |Return Type|Name|Description|
 |--:|---|---|
 |FRotator|Prediction(<br>const float BulletSpeed,<br>const float BulletGravityScale,<br>const float TargetGravityScale,<br>const FVector& From,<br>const FVector& To,<br>const bool bHighArc<br>)|Calculate predicted shooting direction<br><br>BulletGravityScale - Set the value of GravityScale set for the bullet to be shot<br>TargetGravityScale - Set the value of GravityScale set for Target|
 |FVector|PredictPos(<br>const float BulletSpeed,<br>const float BulletGravityScale,<br>const float TargetGravityScale,<br>const FVector& From,<br>const FVector& To,<br>const bool bHighArc<br>)|Calculate predicted position<br><br>BulletGravityScale - Set the value of GravityScale set for the bullet to be shot<br>TargetGravityScale - Set the value of GravityScale set for Target|
 
## {Circular, CharacterCircular} FCS SceneComponent
***If Character's AirControl value is fairly low, CharacterLinearFCS may be used during jumping 
(When the AirControl value is low, it is almost linear movement during jumping)***  
<br />
***How to use CharacterLinearFCS and CharacterCircularFCS together*** &rarr; [Tutorial Video](https://www.youtube.com/watch?v=YHbEk__dcUI)
### `Variables`

 |Type|Name|Description|
 |--:|---|---|
 |int32|Accuracy|Accuracy of prediction calculation|
 |float|ObserverTickInterval|Observe the target at the interval|
 |ECollisionChannel|TraceChannel|Trace channel for measuring the height of the landing point|
 |float|OffsetFromCollisionSurface|Offset value when the predicted point collides with the surface (Default = 50)|
 |IAngularObservable|Observer|Object implementing IAngularObservable|
 
### `Functions`

 |Return Type|Name|Description|
 |--:|---|---|
 |FRotator|Prediction(<br>const float BulletSpeed,<br>const float BulletGravityScale,<br>const float TargetGravityScale,<br>const FVector& From,<br>const FVector& To,<br>const bool bHighArc<br>)|Calculate predicted shooting direction<br><br>BulletGravityScale - Set the value of GravityScale set for the bullet to be shot<br>TargetGravityScale - Set the value of GravityScale set for Target|
  |FVector|PredictPos(<br>const float BulletSpeed,<br>const float BulletGravityScale,<br>const float TargetGravityScale,<br>const FVector& From,<br>const FVector& To,<br>const bool bHighArc<br>)|Calculate predicted position<br><br>BulletGravityScale - Set the value of GravityScale set for the bullet to be shot<br>TargetGravityScale - Set the value of GravityScale set for Target|
 
## SMA {Velocity, Angular} Measurer SceneComponent
### `Variables`

|Type|Name|Description|
|--:|---|---|
|int32|NumOfFrames|Number of frames to be recorded by SMA|
|int32|CurrentIndex|Index representing the latest data|
|TArray&lt;float&gt;|{Velocity, Angular} RecordingArray|Recording array|

## EMA {Velocity, Angular} Measurer SceneComponent
### `Variables`

|Type|Name|Description|
|--:|---|---|
|float|SmoothingFactor|Smoothing factor of EMA|

## VelocityObservable Interface
### `Functions`

|Return Type|Name|Description|
|--:|---|---|
|void|SetTarget(<br>AActor* Target<br>)|Set target|
|AActor*|GetTarget()|Get target|
|float|GetZVelocity()|Get speed in the Z direction when moving on a slope or the like (Character only)|
|float|GetZAcceleration()|Get acceleration in the Z direction when moving on a slope or the like (Character only)|
|float|GetJumpVelocity()|Get speed in the Z direction when jumping (Character only)|
|float|GetVelocity()|Get velocity|
|float|GetAcceleration()|Get acceleration|

## AngularObservable Interface
### `Functions`

|Return Type|Name|Description|
|--:|---|---|
|void|SetTarget(<br>AActor* Target<br>)|Set target|
|AActor*|GetTarget()|Get target|
|float|GetZVelocity()|Get speed in the Z direction when moving on a slope or the like (Character only)|
|float|GetZAcceleration()|Get acceleration in the Z direction when moving on a slope or the like (Character only)|
|float|GetJumpVelocity()|Get speed in the Z direction when jumping (Character only)|
|float|GetAngularVelocity()|Get angular velocity (radian)|
|float|GetAngularAcceleration()|Get angular acceleration (radian)|
|TArray&lt;FVector&gt;|GetLocations()|Prev 3 locations (Index 0 -> the oldest position, Index 2 -> Newest position)|

## VelocityMeasurable Interface
By implementing this interface and attaching to the {CharacterLinear, Linear} FCS component, you can calculate predicted shots with your own measurement method
### `Functions`

|Return Type|Name|Description|
|--:|---|---|
|void|Reset(<br>const AActor* const Target<br>)|Reset the measurement|
|void|SetFlyingMode(<br>const bool bIsFlyingMode<br>)|False if attached to CharacterFCS, true is passed otherwise|
|bool|Measure(<br>const AActor* const Target,<br>float& OutVelocity,<br>float& OutAcceleration,<br>float& OutZVelocity,<br>float& OutZAcceleration,<br>float& OutJumpVelocity<br>)|Measure the target (The return value is a dummy parameter)|

## AngularMeasurable Interface
By implementing this interface and attaching to the {CharacterCircular, Circular} FCS component, you can calculate predicted shots with your own measurement method
### `Functions`

|Return Type|Name|Description|
|--:|---|---|
|void|Reset(<br>const AActor* const Target<br>)|Reset the measurement|
|void|SetFlyingMode(<br>const bool bIsFlyingMode<br>)|False if attached to CharacterFCS, true is passed otherwise|
|bool|Measure(<br>const AActor* const Target,<br>float& OutAngularVelocity,<br>float& OutAngularAcceleration,<br>float& OutZVelocity,<br>float& OutZAcceleration,<br>float& OutJumpVelocity,<br>TArray&lt;FVector&gt;& OutLocations,<br>int32& OutStartIndex<br>)|Measure the target (The return value is a dummy parameter)|

