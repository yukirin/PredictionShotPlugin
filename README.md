# [UE4 Marketplace] PredictionShotPlugin
[UE4 Marketplace] Prediction Shot Plugin Document
# Tutorial
[Demo Video](https://www.youtube.com/watch?v=BrCKP1JALYU)  
[Tutorial Video](https://www.youtube.com/watch?v=YHbEk__dcUI)
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
 |float|BiasFromGround|Z direction bias from the ground to adjust the predicted shooting point|
 |IVelocityObservable|Observer|Object implementing IVelocityObservable|
 
### `Functions`

 |Return Type|Name|Description|
 |--:|---|---|
 |FRotator|Prediction(<br>const float BulletSpeed,<br>const float BulletGravityScale,<br>const float TargetGravityScale,<br>const FVector& From,<br>const FVector& To<br>)|Calculate predicted shooting direction|
 
## {Circular, CharacterCircular} FCS SceneComponent
### `Variables`
 |Type|Name|Description|
 |--:|---|---|
 |int32|Accuracy|Accuracy of prediction calculation|
 |float|ObserverTickInterval|Observe the target at the interval|
 |ECollisionChannel|TraceChannel|Trace channel for measuring the height of the landing point|
 |float|BiasFromGround|Z direction bias from the ground to adjust the predicted shooting point|
 |IAngularObservable|Observer|Object implementing IAngularObservable|
### `Functions`
 |Return Type|Name|Description|
 |--:|---|---|
 |FRotator|Prediction(<br>const float BulletSpeed,<br>const float BulletGravityScale,<br>const float TargetGravityScale,<br>const FVector& From,<br>const FVector& To<br>)|Calculate predicted shooting direction
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
|TArray&lt;FVector&gt;|GetLocations()|Position of the last 3 frames|
|int32|GetStartIndex()|An index representing the oldest position among the data acquired by the above GetLocations
## VelocityMeasurable Interface
By implementing this interface and attaching to the {CharacterLinear, Linear} FCS component, you can calculate predicted shots with your own measurement method
### `Functions`
|Return Type|Name|Description|
|--:|---|---|
|void|Reset(<br>const AActor*,<br>const Target<br>)|Reset the measurement|
|void|SetFlyingMode(<br>const bool bIsFlyingMode<br>)|False if attached to CharacterFCS, true is passed otherwise|
|bool|Measure(<br>const AActor* const Target,<br>float& OutVelocity,<br>float& OutAcceleration,<br>float& OutZVelocity,<br>float& OutZAcceleration,<br>float& OutJumpVelocity<br>)|Measure the target (The return value is a dummy parameter)|
## AngularMeasurable Interface
By implementing this interface and attaching to the {CharacterCircular, Circular} FCS component, you can calculate predicted shots with your own measurement method
### `Functions`
|Return Type|Name|Description|
|--:|---|---|
|void|Reset(<br>const AActor*,<br>const Target<br>)|Reset the measurement|
|void|SetFlyingMode(<br>const bool bIsFlyingMode<br>)|False if attached to CharacterFCS, true is passed otherwise|
|bool|Measure(<br>const AActor* const Target,<br>float& OutAngularVelocity,<br>float& OutAngularAcceleration,<br>float& OutZVelocity,<br>float& OutZAcceleration,<br>float& OutJumpVelocity,<br>TArray&lt;FVector&gt;& OutLocations,<br>int32& OutStartIndex<br>)|Measure the target (The return value is a dummy parameter)|
