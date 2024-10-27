# Delete unrelated steps

The "Delete Unrelated Steps" feature allows you to bulk delete steps that are not needed to prove 
main steps of the proof.

This need may arise when you are working on a proof, and you don't know how to prove some statement.
You may try several different approaches to prove that statement. 
Each unsuccessful attempt produces new steps in the editor, which don't contribute to the target proof. 
Such useless steps may be deleted using the "Delete unrelated steps" functionality.

In order to delete unrelated steps:
1. Select the "root" steps you want to keep in the editor. 
Other steps which participate (directly or transitively) in the proof of the selected "root" steps
will be kept automatically, so you don't have to select them.
Also, hypothesis steps, the goal step, and all [bookmarked](bookmark_steps.md) steps will be kept,
so you don't have to select them as well.
2. Select the "Delete unrelated steps" in the "hamburger" menu in the Editor. 

This works similar to garbage collector in some programming languages.

There is another similar menu item "Delete unrelated steps and hypotheses".
It works the same way, except that it will also remove unrelated hypothesis steps.