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
## {Circular, CharacterCircular} FCS SceneComponent
## SMA {Velocity, Angular} Measurer SceneComponent
## EMA {Velocity, Angular} Measurer SceneComponent
## IVelocityObservableInterface
## IAngularObservableInterface
