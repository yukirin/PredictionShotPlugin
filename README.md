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
 |FRotator|Prediction(<br>const float BulletSpeed,<br>const float BulletGravityScale,<br>const float TargetGravityScale,<br>const FVector& From,<br>const FVector& To)|Calculate predicted shooting direction|
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
 |FRotator|Prediction(<br>const float BulletSpeed,<br>const float BulletGravityScale,<br>const float TargetGravityScale,<br>const FVector& From,<br>const FVector& To)|Calculate predicted shooting direction
## SMA {Velocity, Angular} Measurer SceneComponent
### `Variables`
### `Functions`
## EMA {Velocity, Angular} Measurer SceneComponent
### `Variables`
### `Functions`
## VelocityObservable Interface
### `Functions`
## AngularObservable Interface
### `Functions`
## VelocityMeasurable Interface
By implementing this interface and attaching to the {CharacterLinear, Linear} FCS component, you can calculate predicted shots with your own measurement method
### `Functions`
## AngularMeasurable Interface
By implementing this interface and attaching to the {CharacterCircular, Circular} FCS component, you can calculate predicted shots with your own measurement method
### `Functions`
