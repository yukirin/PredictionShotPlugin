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
### `Functions`
## {Circular, CharacterCircular} FCS SceneComponent
### `Variables`
### `Functions`
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
