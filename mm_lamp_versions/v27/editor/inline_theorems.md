# Inline theorems

The "Inline theorems" feature allows to replace a single step with multiple steps of the proof of the
theorem used by that single step. The overall proof in the editor will stay valid
(except some small inconsistencies which can be easily fixed, see below). 
This feature changes multiple steps at once. 
You select what theorems to inline, and then all steps using these theorems will be inlined.

To inline theorems:
1. Make sure all steps you want to inline the proof for are marked with a green check mark.
If they are not, try to "unify all".
2. Select the "Inline theorems" in the "hamburger" menu in the editor.
3. In the opened dialog select all theorems you want to inline and click Ok.
4. In the opened another dialog, click Ok to confirm the list of theorems you selected.

This will inline all occurrences of the selected theorems in the editor.
However, this feature is not recursive.
Let's say, you want to inline theorems A and B.
If theorem B uses A, then after inlining of A and B, theorem A will be still present in the editor 
(that will be another occurrence of A, coming from B).
So, if you want to completely get rid of some particular theorems in your proof, 
then repeat the inlining procedure until all unwanted theorems disappear.

If you have a long list of theorems in your proof, you can filter them by label in the theorem selection dialog.

Often the inlining procedure introduces two types of inconsistencies in your proof: 
duplicated steps and incorrect order of steps 
(for example, step 2 depends on step 1, but step 1 is located after step 2).
This can be easily fixed by 
[Merge similar steps](merge_similar_steps.md)
and [Reorder steps automatically](reorder_steps_automatically.md).