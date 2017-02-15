# Comparison

As with most patterns, I think we should not view Higher Order Components or Functions as Child Components as silver bullets to _**always**_ be applied when we encounter a problem with reusability or abstraction.

Here are a few points I use when evaluating _**when**_ to use a HOC or FaCC.

| Do your consumers need to have . . . | Higher Order Components \(HOC\) | Functions as Child Components \(FaCC\) |
| :--- | :--- | :--- |
| Knowledge of HOC internals | If your consumer **does not need to know** that you are not _actually_ using the original React Component, HOCs are useful to _hide that abstraction_.  |  |
| Power over composition |  | If you require more power over composition in the consumer, Functions as Child Component or render props allow you a lot of flexibility in the render method! |



