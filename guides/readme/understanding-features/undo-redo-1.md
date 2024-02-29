# Undo redo

### Overview

A feature that help user can playback their actions with correct layout and data.

Contributors you can contact: Edgar, Harry

***

### Mechanism

#### Storage data

* Using `stage` object to storage the whole user's steps.
* Using `viewUndoRedoProxy` to save status of feature.
* Update status of undo redo by using `Proxy` with target is `viewUndoRedoProxy`.

***

#### Steps

* Each `step` has specific parameters to storage data of implement processing.
* Please refer `step.ts` file in `pfcore` to know more about specific step and how many steps are there in PF.
* `addStep:` push at least 1 suitable step to `stage` when user performs an action.

***

### Note

Because undo redo feature cover the whole actions in PF editor so when you update another feature or fix bug, please re-check undo redo with those related actions.
