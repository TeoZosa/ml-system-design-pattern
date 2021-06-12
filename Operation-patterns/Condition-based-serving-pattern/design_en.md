# Condition-Based Serving Pattern

## Use Case

- When prediction targets demonstrate high condition-based variance.
- When models can be conditionally selected in a rule-based manner.

## Architecture

The Condition-Based Serving Pattern is an architecture to select a model based on a
condition.

This is useful in situations where the prediction target varies depending on a user's
condition, like time, place, or persona.

- For instance, a food-recommendation ML model should probably not recommend steak and
  wine for a morning meal.
- Similarly, given a picture of a bridge, an image-based landmark-classification model
  being used on a device located in Japan should probably assign a low probability that
  the bridge in the picture is the Golden Gate Bridge, which is located in California.

To exploit these conditional dependencies, each condition may have a corresponding
prediction service with selection accomplished by a reverse proxy.

- The selection rule may depend on the specific use case: for time-based model
  selection, you may need a morning, noon, and evening model for those respective times.

- Model development difficulty depends on how the problem space and target variables
  change with respect to the different conditions; If feature engineering may be shared
  across models, you may only need to update the target variables for each condition.
  Otherwise, using independent models or eschewing this pattern altogether may be
  necessary. Note however that since each condition-specific model essentially overfits
  to that condition, model performance is generally better compared to a general model.

- Model evaluation, improvement, and management increases proportionally with the number
  of models being used. This pattern may become less feasible as the number of models
  increases, so be sure that this pattern is the correct solution to the problem at
  hand.

- Separating conditions depends on the variability between model input, features, and
  target. For instance, it may be possible to use the same model for morning and
  evening. On the other hand, conditional separation highly incongruent with users' 
  expectations may be a significant operational mistake.

## Diagram

![diagram](diagram.png)

## Pros

- Select an adequate model depending on condition.

## Cons

- Operational cost raise with number of models.

## Considerations

- How to separate condition.
- Balance between number of models and model management.

## Sample

https://github.com/shibuiwilliam/ml-system-in-actions/tree/main/chapter6_operation_management/condition_based_pattern
